# Apart YÖnetim Sistemi
#include<stdio.h>
#include<string.h>

int main()
{
    int secenek; // secenek değişkeninin türü ifade edilmektedir.
    printf("\nYeni kiracı kaydı için 1'i seçiniz");
    printf("\nÖgrenci kaydini silmek icin 2'i seciniz.");
    printf("\nÖgrenci bilgilerini guncellemek icin 3'u seciniz.");
    printf("\nÖgrenci bilgilerini isim sırası A-Z’ye olacak biçimde listelemek için 4'u seciniz");
    printf("\nÖgrenci borc bilgilerini listelemek için 5’i seciniz.");
    printf("\nKira borcu odemek icin 6'i seciniz.");
    printf("\nElektrik borcu odemek icin 7'i seciniz.");
    printf("\nCikis yapmak icin 8’i seciniz.");
    scanf("%d", &secenek); //kullanıcıdan seçimi istenmektedir.
    
    if(secenek==1) //kullanıcının seçimine göre ilgili işlem yapılmaktadır.
    {
        ekleme(); //kullanıcı 1.seçeneği seçtiği takdirde kiracı ekleme yapılmaktadır.
    }
    else if(secenek==2)
    {
    printf(":idler:\n"); // girilen kiracı id leri yazılmaktadır.
    liste();
    silme();
    }
    
    return 0;
}

void ekleme() //Fonksiyonların prototipleri deklare edilmektedir.
{
    FILE *olustur;
    int id, tc;
    char ad[50], soyad[50],cinsiyet[50],telefon[50],eposta[50],dogumtarihi[50],apartgirisgun[50],apartgirisay[50],apartgirisyil[50];

    printf("\nid giriniz:");
    scanf("%d", &id); //kullanıcıdan id girmesi istenmektedir.
    printf("\ntc giriniz:");
    scanf("%d", &tc);  //kullanıcıdan tc  girmesi istenmektedir.
    printf("\nadını giriniz:");
    scanf("%s", ad);  //kullanıcıdan ad girmesi istenmektedir.
    printf("\nsoyadını giriniz:");
    scanf("%s", soyad);  //kullanıcıdan soyad girmesi istenmektedir.
    printf("\n(e/k)cinsiyet giriniz:");
    scanf("%s", cinsiyet);  //kullanıcıdan cinsiyet girmesi istenmektedir.
    printf("\ndoğum tarihini(gün/ay/yil) giriniz:");
    scanf("%s", dogumtarihi);  //kullanıcıdan doğum tarihi girmesi istenmektedir.
    printf("\ntelefonunu giriniz:");
    scanf("%s", telefon);  //kullanıcıdan telefon numarası girmesi istenmektedir.
    printf("\nepostasını giriniz:");
    scanf("%s", eposta);  //kullanıcıdan e-posta adresi girmesi istenmektedir.
    printf("\naparta giriş gününü giriniz:");
    scanf("%s", apartgirisgun);  //kullanıcıdan aparta giriş günü girmesi istenmektedir.
    printf("\naparta giriş ayını (Ocak için 1 , Aralık için 12) giriniz:");
    scanf("%s", apartgirisay);  //kullanıcıdan aparta giriş ayı girmesi istenmektedir.
    printf("\naparta giriş yılını giriniz:");
    scanf("%s", apartgirisyil); //kullanıcıdan aparta giriş yılı girmesi istenmektedir.

    olustur = fopen("Ogrenci.txt", "a");  //öğrenci bilgi metnini içeren dosya oluşturulur.               
    fprintf(olustur, "%d %d %s %s %s %s %s %s %s %s %s\n", id, tc, ad, soyad, cinsiyet, dogumtarihi, telefon, eposta, apartgirisgun, apartgirisay, apartgirisyil);
    fclose(olustur);                                    
}


void liste() //Fonksiyonların prototipleri deklare edilmektedir.

{
    FILE *olustur;
    int id;
    char ad[50], soyad[50], tc[50];
    char cinsiyet[50];
    char telefon[50];
    char eposta[50];
    char dogumtarihi[50];
    char apartgirisgun[50];
    char apartgirisay[50];
    char apartgirisyil[50];

    olustur = fopen("Ogrenci.txt", "r"); 
    while (fscanf(olustur, "%d %d %s %s %s %s %s %s %s %s %s\n", &id, tc, ad, soyad, cinsiyet, dogumtarihi, telefon, eposta, apartgirisgun, apartgirisay, apartgirisyil) != EOF)
    {                       
        printf("%d\n", id); 
    }
    fclose(olustur); 
}


void silme() //Fonksiyonların prototipleri deklare edilmektedir.
{
    FILE *olustur, *tutulan;
    int id, girilenId;
    char ad[50], soyad[50], tc[50];
    char cinsiyet[50];
    char telefon[50];
    char eposta[50];
    char dogumtarihi[50];
    char apartgirisgun[50];
    char apartgirisay[50];
    char apartgirisyil[50];
    printf("Silinecek Ogrenci ID: ");
    scanf("%d", &girilenId);

    olustur = fopen("Ogrenci.txt", "r");        
    tutulan = fopen("Ogrenci_Temp.txt", "a"); 

    
   while (fscanf(olustur, "%d %s %s %s %s %s %s %s %s %s %s\n", &id, tc, ad, soyad, cinsiyet, dogumtarihi, telefon, eposta, apartgirisgun, apartgirisay, apartgirisyil) != EOF)
    {
        if (id != girilenId) 
        {                                                    
            fprintf(tutulan, "%d %s %s %s %s %s %s %s %s %s %s\n", id, tc, ad, soyad, cinsiyet, dogumtarihi, telefon, eposta, apartgirisgun, apartgirisay, apartgirisyil); 
        }
    }

    fclose(olustur); 
    fclose(tutulan);

    remove("Ogrenci.txt");                     
    rename("Ogrenci_Temp.txt", "Ogrenci.txt"); 
}

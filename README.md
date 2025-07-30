# Apart YÖnetim Sistemi
#include<stdio.h>

#include<string.h>

int main()
{

    int secenek; 
    printf("\nYeni kiracı kaydı için 1'i seçiniz");
    printf("\nÖgrenci kaydini silmek icin 2'i seciniz.");
    printf("\nÖgrenci bilgilerini guncellemek icin 3'u seciniz.");
    printf("\nÖgrenci bilgilerini isim sırası A-Z’ye olacak biçimde listelemek için 4'u seciniz");
    printf("\nÖgrenci borc bilgilerini listelemek için 5’i seciniz.");
    printf("\nKira borcu odemek icin 6'i seciniz.");
    printf("\nElektrik borcu odemek icin 7'i seciniz.");
    printf("\nCikis yapmak icin 8’i seciniz.");
    scanf("%d", &secenek); 
    
    if(secenek==1) 
    {
        ekleme(); 
    }
    else if(secenek==2)
    {
    printf(":idler:\n"); 
    liste();
    silme();
    }
    
    return 0;
}

void ekleme()

{

    FILE *olustur;
    
    int id, tc;
    
    char ad[50], soyad[50],cinsiyet[50],telefon[50],eposta[50],dogumtarihi[50],apartgirisgun[50],apartgirisay[50],apartgirisyil[50];

    printf("\nid giriniz:");
    scanf("%d", &id); 
    printf("\ntc giriniz:");
    scanf("%d", &tc); 
    printf("\nadını giriniz:");
    scanf("%s", ad);  
    printf("\nsoyadını giriniz:");
    scanf("%s", soyad);  
    printf("\n(e/k)cinsiyet giriniz:");
    scanf("%s", cinsiyet);  
    printf("\ndoğum tarihini(gün/ay/yil) giriniz:");
    scanf("%s", dogumtarihi);  
    printf("\ntelefonunu giriniz:");
    scanf("%s", telefon);  
    printf("\nepostasını giriniz:");
    scanf("%s", eposta);  
    printf("\naparta giriş gününü giriniz:");
    scanf("%s", apartgirisgun);  
    printf("\naparta giriş ayını (Ocak için 1 , Aralık için 12) giriniz:");
    scanf("%s", apartgirisay);  
    printf("\naparta giriş yılını giriniz:");
    scanf("%s", apartgirisyil); 

    olustur = fopen("Ogrenci.txt", "a");  //öğrenci bilgi metnini içeren dosya oluşturulur.               
    fprintf(olustur, "%d %d %s %s %s %s %s %s %s %s %s\n", id, tc, ad, soyad, cinsiyet, dogumtarihi, telefon, eposta, apartgirisgun, apartgirisay, apartgirisyil);
    fclose(olustur);                                    
}


void liste()

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


void silme() 
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

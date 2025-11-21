#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main() {
    // Rastgele sayı üretimi için çekirdek oluşturma
    srand(time(NULL));

    // 4. Durum Yönetimi Değişkenleri
    int saglik = 85;
    int enerji = 75;
    int yemek = 0;
    int siginak = 0; // Sığınak sayısı
    char komut;
    char sifre_giris;

    printf("HAYATTA KALMA SIMULATORU\n");
    printf("Komutlar: [A]vlan, [S]iginak, [R]Dinlen, [E]nvanter, [F]Tehlike, [P]Sifre, [X]Cikis\n");

    // Oyun Döngüsü
    do {
        printf("\nKomut giriniz: ");
        scanf(" %c", &komut);

        if(komut >= 'a' && komut <= 'z') {
            komut = komut - 32;
        }

        switch (komut) {
            case 'A': // AVLANMA
                if (enerji >= 15) {
                    enerji -= 15; 
                    printf("Avlanmaya ciktin... (Enerji -15)\n");

                    int sans = rand() % 100;
                    if (sans < 40) {
                        yemek++;
                        printf("Basarili! Bir yemek buldun. (Yemek: %d)\n", yemek);
                    } 
                    else if (sans > 80) {
                        saglik -= 20;
                        printf("Dikkat! Vahsi bir hayvan saldirdi. (Saglik -20)\n");
                    } else {
                        printf("Hicbir sey bulamadan dondun.\n");
                    }
                } else {
                    printf("Avlanmak icin yeterli enerjin yok! (Gereken: 15)\n");
                }
                break;

            case 'S': // SIĞINAK ARA
                if (enerji >= 10) {
                    enerji -= 10;
                    int sans = rand() % 100;
                    if (sans < 30) { // %30 şans
                        siginak++; 
                        printf("Basarili! Yeni bir siginak kurdun. (Toplam Siginak: %d)\n", siginak);
                    } else {
                        printf("Uygun bir yer bulamadin.\n");
                    }
                } else {
                    printf("Aramak icin enerjin yok.\n");
                }
                break;

            case 'R': // DİNLEN
                if (siginak > 0) {
                    enerji += 30;
                    saglik += 10;
                    printf("Siginaklarindan birinde guzelce uyudun. (Enerji +30, Saglik +10)\n");
                } else {
                    enerji += 15;
                    printf("Disarida tedirgin bir sekilde dinlendin. (Enerji +15)\n");
                }
                
                if(enerji > 100) enerji = 100;
                if(saglik > 100) saglik = 100;
                break;

            case 'E': // ENVANTER
                printf("\n--- DURUM ---\n");
                printf("Saglik : %d\n", saglik);
                printf("Enerji : %d\n", enerji);
                printf("Yemek  : %d\n", yemek);
                printf("Siginak Sayisi: %d\n", siginak);
                break;

            case 'F': // TEHLİKE DALGASI
                printf("TEHLIKE DALGASI GELIYOR!\n");
                int hasar;
                int i; // Değişkeni döngüden önce tanımladık (Hata çıkmaması için)
                for (i = 1; i <= 3; i++) {
                    hasar = rand() % 10 + 1; 
                    saglik -= hasar;
                    printf("%d. Dalga vurdu! %d hasar aldin.\n", i, hasar);
                }
                printf("Tehlike gecti. Guncel Saglik: %d\n", saglik);
                break;

            case 'P': // ŞİFRELİ İLERLEME
                printf("Onunde kilitli bir kapi var. Gecmek icin '1' tusuna basmalisin.\n");
                do {
                    printf("Sifreyi gir: ");
                    scanf(" %c", &sifre_giris);
                    if(sifre_giris != '1') {
                        printf("Yanlis sifre! Tekrar dene.\n");
                    }
                } while (sifre_giris != '1');
                printf("Kapi acildi! Engeli astin.\n");
                break;

            case 'X': // ÇIKIŞ
                printf("Simulasyondan cikiliyor...\n");
                break;

            default:
                printf("Gecersiz komut! Listeden bir komut secin.\n");
        }

        if (saglik <= 0) {
            printf("\nOLDUN! Hayatta kalamadin.\n");
            break; 
        }

    } while (komut != 'X'); 

    printf("Oyun Bitti.\n");
    return 0;
}# hayatta-kalma-oyunu

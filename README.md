Oy Kullanma Simülasyonu
using System;

class Program
{
    static void Main()
    {
        // Seçmen listesi
        string[] voters = new string[20];

        // Seçmen bilgilerini giriş
        for (int i = 0; i < voters.Length; i++)
        {
            Console.WriteLine($"Seçmen {i + 1} Bilgileri:");

            Console.Write("Adınız: ");
            string name = Console.ReadLine();

            Console.Write("Mezuniyet Durumu (doktora, lisans, lise, ortaokul, ilkokul, yok): ");
            string education = Console.ReadLine().ToLower();

            voters[i] = $"{name} - {education}";
        }

        // Oy kullanma işlemi
        for (int i = 0; i < voters.Length; i++)
        {
            double aCoefficient = GetACoefficient(voters[i]);
            double bCoefficient = GetBCoefficient(i);

            // Parti puanları hesaplanıyor (örneğin)
            double party1Points = 10 * aCoefficient * bCoefficient;
            double party2Points = 8 * aCoefficient * bCoefficient;
            double party3Points = 6 * aCoefficient * bCoefficient;

            // Toplam puanları ekrana yazdırma (örneğin)
            Console.WriteLine($"{voters[i]} - Parti 1: {party1Points}, Parti 2: {party2Points}, Parti 3: {party3Points}");
        }

        // Sonuçları değerlendirme ve kazananı belirleme (örneğin)
        Console.WriteLine("Seçim Sonuçları:");
        DetermineWinner(voters);

        Console.ReadLine(); // Uygulamanın kapanmaması için bekleme
    }

    static double GetACoefficient(string voterInfo)
    {
        string[] infoArray = voterInfo.Split('-');
        string education = infoArray[1].Trim();

        switch (education)
        {
            case "doktora":
                return 5;
            case "lisans":
            case "yükseklisans":
                return 4;
            case "lise":
                return 3;
            case "ortaokul":
                return 2;
            case "ilkokul":
                return 1;
            case "yok":
                return 0.5;
            default:
                return 0;
        }
    }

    static double GetBCoefficient(int votingHour)
    {
        // Saat 8'de B katsayısı en yüksek (10), saat 18'de en düşük (1)
        double maxCoefficient = 10;
        double minCoefficient = 1;

        // Saat 8-18 arasındaki saatlere göre B katsayısını hesapla
        return maxCoefficient - (votingHour * ((maxCoefficient - minCoefficient) / 10));
    }

    static void DetermineWinner(string[] voters)
    {
        // Parti puanlarını hesapla (örneğin)
        double party1TotalPoints = 0;
        double party2TotalPoints = 0;
        double party3TotalPoints = 0;

        for (int i = 0; i < voters.Length; i++)
        {
            double aCoefficient = GetACoefficient(voters[i]);
            double bCoefficient = GetBCoefficient(i);

            party1TotalPoints += 10 * aCoefficient * bCoefficient;
            party2TotalPoints += 8 * aCoefficient * bCoefficient;
            party3TotalPoints += 6 * aCoefficient * bCoefficient;
        }

        // Kazananı belirle
        if (party1TotalPoints > party2TotalPoints && party1TotalPoints > party3TotalPoints)
        {
            Console.WriteLine("Parti 1 kazandı!");
        }
        else if (party2TotalPoints > party1TotalPoints && party2TotalPoints > party3TotalPoints)
        {
            Console.WriteLine("Parti 2 kazandı!");
        }
        else if (party3TotalPoints > party1TotalPoints && party3TotalPoints > party2TotalPoints)
        {
            Console.WriteLine("Parti 3 kazandı!");
        }
        else
        {
            Console.WriteLine("Seçim berabere sonuçlandı!");
        }
    }
}

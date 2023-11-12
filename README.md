# help
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Darbininkai
{
    class Darbas
    {
        private string įmonė;
        private int metai;
        private int mėn;
        private int diena;
        private string pavard;
        private string pavad;
        private double įkainis;
        private int vnt;       

        public Darbas(string įmonė, int metai, int mėn, int diena, string pavard, string pavad, double įkainis, int vnt)
        {
            this.įmonė = įmonė;
            this.metai = metai;
            this.mėn = mėn;
            this.diena = diena;
            this.pavard = pavard;
            this.pavad = pavad;
            this.įkainis = įkainis;
            this.vnt = vnt;
        }

        public override string ToString()
        {
            string eilute;
            eilute = string.Format("|  {0, -11} |  {1, -6:d} | {2, -5:d} | {3, -3:d} | {4, 3} | {5, 7}  | {6, 2:f2} | {7, 5:d} |",
            įmonė, metai, mėn, diena, pavard, pavad, įkainis, vnt);
            return eilute;
        }

        public override bool Equals(object objektas)
        {           
            Darbas darbas = objektas as Darbas;
            return darbas.pavard == pavard;            
        }

        public override int GetHashCode()
        {
            return base.GetHashCode();
        }

        public string ImtiPavard()
        {
            return pavard;
        }

        public int ImtiMetus()
        {
            return metai;
        }

        public int ImtiMenesius()
        {
            return mėn;
        }

        public int ImtiDienas()
        {
            return diena;
        }

        public int ImtiDetaliųSk()
        {
            return vnt;
        }

        public double Uždarbis()
        {
            return įkainis * vnt;
        }

    }

    class DarboMasyvas
    {
        const int Cn = 50;
        private Darbas[] Darbai; //Darbininkų atlikto darbo informacija
        private int n; //Darbų rezultatų kiekis

        public DarboMasyvas()
        {
            Darbai = new Darbas[Cn];
            n = 0;
        }

        public Darbas ImtiDuomenis(int i)
        {
            return Darbai[i];
        }

        public int ImtiSkaičių()
        {
            return n;
        }

        public void DėtiDarbą(Darbas darbai)
        {
            Darbai[n++] = darbai;
        }
        public Darbas RastiDaugiausiaiUždirbantįDarbuotoją()
        {
            Darbas daugiausiaiUždirbantis = Darbai[0];             
            foreach (Darbas darbuotojas in Darbai)
            {           
                if (darbuotojas.Uždarbis() > daugiausiaiUždirbantis.Uždarbis())
                {                    
                    daugiausiaiUždirbantis = darbuotojas;
                }
            }
            return daugiausiaiUždirbantis;
        }


    }

    class MaxDarbas
    {
        private int n;
        private Darbas[] D;
        const int Cn = 50;
        private string pavarde;
        private int dienos;
        private int vnt;
        private double uždarbis;

        public MaxDarbas()
        {
            D = new Darbas[Cn];
            n = 0;
            pavarde = "";
            dienos = 0;
            vnt = 0;
            uždarbis = 0;
        }

        public Darbas Imti(int i)
        {
            return D[i];
        }

        public int Imti()
        {
            return n;
        }

        public string ImtiPavard()
        {
            return pavarde;
        }

        public int ImtiDienas()
        {
            return dienos;
        }

        public int ImtiDetaliuKiek()
        {
            return vnt;
        }

        public double ImtiUzdarbi()
        {
            return uždarbis;
        }
        
        public void Deti(string pavarde, int dienos, int vnt, double uždarbis, Darbas d)
        {
            D[n++] = d;
            this.pavarde = pavarde;
            this.dienos = dienos;
            this.vnt = vnt;
            this.uždarbis = uždarbis;
        }
        
    }

    internal class Program
    {
        const string CFd = "..\\..\\Darbas.txt";
        const string CFr = "..\\..\\DarboRezultatai.txt";        
        static void Main(string[] args)
        {
            DarboMasyvas darbas = new DarboMasyvas();
            MaxDarbas maxDarbas = new MaxDarbas();
            
            if (File.Exists(CFr))
                File.Delete(CFr);
            Skaityti(CFd, darbas);
            Spausdinti(CFr, darbas);
            MaxUždarbis(darbas, maxDarbas); 
            
        }

        static void Skaityti(string fv, DarboMasyvas darbai)
        {
            int i = 0;
            using (StreamReader reader = new StreamReader(fv))
            {
                string line;
                while ((line = reader.ReadLine()) != null)
                {
                    string[] parts = line.Split(';');
                    string įmonė = parts[0];
                    int metai = int.Parse(parts[1]);
                    int mėn = int.Parse(parts[2]);
                    int diena = int.Parse(parts[3]);
                    string pavard = parts[4];
                    string pavad = parts[5];
                    double įkainis = double.Parse(parts[6]);
                    int vnt = int.Parse(parts[7]);
                    Darbas D = new Darbas(įmonė, metai, mėn, diena, pavard, pavad, įkainis, vnt);
                    darbai.DėtiDarbą(D);
                    i++;
                }
            }
        }

        static void Spausdinti(string fv, DarboMasyvas darbai)
        {
            string viršus = "                     Informacija apie darbininkų darbo rezultatus       \r\n"
                           + "----------------------------------------------------------------------------------------------------\r\n"
                           + "|   Įmonės     |  Metai  |  Mėnesis | Diena |  Darbininko  |   Detalės    |  Įkainis  |  Pagamintų  |\r\n"
                           + "| pavadinimas  |         |          |       |   pavardė    |  pavadinimas |           |   detalių   |\r\n"
                           + "|              |         |          |       |              |              |           |   skaičius  |\r\n"
                           + "----------------------------------------------------------------------------------------------------";
            using (var fr = File.AppendText(fv))
            {
                fr.WriteLine(viršus);
                for (int i = 0; i < darbai.ImtiSkaičių(); i++)
                {
                    fr.WriteLine(darbai.ImtiDuomenis(i).ToString());
                }
                fr.WriteLine("----------------------------------------------------------------------------------------------------");
            }
        }

        /*static void PapildytiDarb(DarboMasyvas darbai)
        {
            MaxDarbas maxDarbas = new MaxDarbas();

            for (int i = 0; i < darbai.ImtiSkaičių(); i++)
            {
                Darbas darbas = darbai.ImtiDuomenis(i);
                bool found = false;

                for (int j = 0; j < maxDarbas.Imti(); j++)
                {
                    Darbas maxDarbininkas = maxDarbas.Imti(j);
                    
                    if (maxDarbininkas.Equals(darbas))
                    {
                        found = true;
                        maxDarbininkas.Uždarbis() += darbas.Uždarbis();
                        maxDarbininkas.ImtiDetaliųSk() += darbas.ImtiDetaliųSk();
                        break;
                    }
                }

                if (!found)
                {
                    maxDarbas.Deti(darbas);
                }
            }
        }*/


        /*static Darbas MaxUždarbis(DarboMasyvas darbai)
        {
            Darbas max = darbai.ImtiDuomenis(0);
            for (int i = 1; i < darbai.ImtiSkaičių(); i++)
            {
                Darbas darb = darbai.ImtiDuomenis(i);
                if (darb.Uždarbis() > max.Uždarbis())
                    max = darb;
            }
            return max;
        }*/


        static int Dienos(DarboMasyvas darbai)
        {
            int dienos = 0;            
            for (int i = 0; i < darbai.ImtiSkaičių(); i++)
            {
                for (int j = 0; j < darbai.ImtiSkaičių() && j != i; j++)
                {
                    if (darbai.ImtiDuomenis(i).Equals(darbai.ImtiDuomenis(j)))
                    {
                        dienos = dienos + ((darbai.ImtiDuomenis(i).ImtiMetus() - darbai.ImtiDuomenis(j).ImtiMetus()) * 365 +
                            (darbai.ImtiDuomenis(i).ImtiMenesius() - darbai.ImtiDuomenis(j).ImtiMenesius()) * 30 +
                            (darbai.ImtiDuomenis(i).ImtiDienas() - darbai.ImtiDuomenis(j).ImtiDienas()));
                    }
                }
            }
            return dienos;
        }

        static int Vnt(DarboMasyvas darbai)
        {
            int vnt = 0;
            for (int i = 0; i < darbai.ImtiSkaičių(); i++)
            {
                for (int j = 0; j < darbai.ImtiSkaičių() && j != i; j++)
                {
                    if (darbai.ImtiDuomenis(i).Equals(darbai.ImtiDuomenis(j)))
                    {
                        vnt = vnt + (darbai.ImtiDuomenis(j).ImtiDetaliųSk() + darbai.ImtiDuomenis(i).ImtiDetaliųSk());
                    }
                }
            }
            return vnt;
        }

        static double Uždarbis(DarboMasyvas darbai)
        {
            double uždarbis = 0;
            for (int i = 0; i < darbai.ImtiSkaičių(); i++)
            {
                for (int j = 0; j < darbai.ImtiSkaičių() && j != i; j++)
                {
                    if (darbai.ImtiDuomenis(i).Equals(darbai.ImtiDuomenis(j)))
                    {
                        uždarbis = uždarbis + (darbai.ImtiDuomenis(j).Uždarbis() + darbai.ImtiDuomenis(i).Uždarbis());
                    }
                }
            }
            return uždarbis;
        }

        static Darbas MaxUždarbis(DarboMasyvas darbai, MaxDarbas maxDarbas)
        {
            Darbas max = darbai.ImtiDuomenis(0);            
            for (int i = 1; i < darbai.ImtiSkaičių(); i++)
            {
                for (int j = 0; j < darbai.ImtiSkaičių(); j++)
                {
                    if (darbai.ImtiDuomenis(i).Equals(darbai.ImtiDuomenis(j)))
                    {
                        maxDarbas.Deti(darbai.ImtiDuomenis(i).ImtiPavard(), Dienos(darbai), Vnt(darbai), Uždarbis(darbai), darbai.ImtiDuomenis(i));                        
                    }
                }
                Console.WriteLine("{0} {1} {2} {3}", maxDarbas.ImtiPavard(), maxDarbas.ImtiDienas(), maxDarbas.ImtiDetaliuKiek(), maxDarbas.ImtiUzdarbi());
                                
            }
            return max;
        }

    }
}

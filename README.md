# help
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Workers
{
    class Work

{

private string company;

private int year;

private int month;

private int day;

private String lastname;

private String name;

private double rate;

private int unit;

public Job(string company, int year, int month, int day, string lastname, string title, double rate, int unit)

{

this.company = company;

this.year = year;

this.month = month;

this.day = day;

this.lastname = lastname;

this.pavad = pavad;

this.rate = rate;

this.unit = unit;

}

public override string ToString()

{

string string;

string = string.Format("| {0, -11} | {1, -6:d} | {2, -5:d} | {3, -3:d} | {4, 3} | {5 , 7} | {6, 2:f2} | {7, 5:d} |",

company, year, month, day, surname, name, rate, unit);

return line;

}

public override bool Equals(object object)

{

Job job = object as Job;

return work.name == name;

}

public override int GetHashCode()

{

return base.GetHashCode();

}

public string GetName()

{

return surname;

}

public int GetYear()

{

return year;

}

public int GetMonths()

{

return month;

}

public int GetDay()

{

return day;

}

public int GetDetails()

{

return unit;

}

public double Earnings()

{

return rate * unit;

}

}

class JobArray

{

const int Cn = 50;

private Job[] Jobs; //Information of work done by workers

private int n; //Number of job results

public WorkArray()

{

Jobs = new Job[Cn];

n = 0;

}

public Job GetData(int i)

{

return Jobs[i];

}

public int GetNumber()

{

return n;

}

public void PutJob(Job jobs)

{

Jobs[n++] = jobs;

}

public Job FindHighestEarningEmployee()

{

Job topEarning = Jobs[0];

foreach (Job employee in Jobs)

{

if (employee.Earnings() > topEarner.Earnings())

{

topEarner = employee;

}

}

return highestEarner;

}

}

class MaxWork

{

private int n;

private Job[] D;

const int Cn = 50;

private String lastname;

private int days;

private int unit;

private double earnings;

public MaxWork()

{

D = new Job[Cn];

n = 0;

lastname = "";

days = 0;

units = 0;

earnings = 0;

}

public Job Take(int i)

{

return D[i];

}

public int Get()

{

return n;

}

public string GetName()

{

return last name;

}

public int GetDay()

{

return days;

}

public int GetDetailQuantity()

{

return unit;

}

public double GetWork()

{

return earnings;

}

public void Deti(string lastname, int days, int units, double earnings, Job d)

{

D[n++] = d;

this.lastname = lastname;

this.days = days;

this.unit = unit;

this.earnings = earnings;

}

}

    internal class Program

{

const string CFd = "..\\..\\Work.txt";

const string CFr = "..\\..\\WorkResults.txt";

static void Main(string[] args)

{

JobArray job = new JobArray();

MaxWork maxWork = new MaxWork();

if (File.Exists(CFr))

File.Delete(CFr);

Read(CFd, job);

Print(CFr, job);

MaxEarnings(work, maxWork);

}

static void Read(string fv, WorkArray works)

{

int i = 0;

using (StreamReader reader = new StreamReader(fv))

{

string line;

while ((line = reader.ReadLine()) != null)

{

string[] parts = line.Split(';');

string company = parts[0];

int year = int.Parse(parts[1]);

int month = int.Parse(parts[2]);

int day = int.Parse(parts[3]);

string lastname = parts[4];

string name = parts[5];

double rate = double.Parse(parts[6]);

int parts = int.Parse(parts[7]);

Job D = new Job(company, year, month, day, last name, first name, rate, unit);

jobs.PutWork(D);

i++;

}

}

}



static void Print(string fv, JobArray jobs)

{

string top = " Information about the work results of workers \r\n"

+ "------------------------------------------------ ---------------------------------------------------- --\r\n"

+ "| Company | Year | Month | Day | Worker | Details | Rate | Produced |\r\n"

+ "| name | | | | last name | name | | details |\r\n"

+ "| | | | | | | | number |\r\n"

+ "------------------------------------------------ ---------------------------------------------------- --";

using (var fr = File.AppendText(fv))

{

fr.WriteLine(top);

for (int i = 0; i < jobs.GetNumber(); i++)

{

fr.WriteLine(jobs.GetData(i).ToString());

}

fr.WriteLine("------------------------------------------------ ---------------------------------------------------- -----");

}

}



static int Days(JobArray jobs)

{

int days = 0;

for (int i = 0; i < jobs.GetNumber(); i++)

{

for (int j = 0; j < jobs.GetNumbers() && j != i; j++)

{

if (jobs.GetData(i).Equals(jobs.GetData(j)))

{

days = days + (((jobs.GetData(i).GetYear() - jobs.GetData(j).GetYear()) * 365 +

(jobs.GetData(i).GetMonth() - jobs.GetData(j).GetMonth()) * 30 +

(jobs.GetData(i).GetDay() - jobs.GetData(j).GetDay()));

}

}

}

return days;

}

static int Units(WorkArray works)

{

int units = 0;

for (int i = 0; i < jobs.GetNumber(); i++)

{

for (int j = 0; j < jobs.GetNumbers() && j != i; j++)

{

if (jobs.GetData(i).Equals(jobs.GetData(j)))

{

vnt = vnt + (jobs.GetData(j).GetDetails() + jobs.GetData(i).GetDetails());

}

}

}

return unit;

}



static double Earnings(WorkArray jobs)

{

double earnings = 0;

for (int i = 0; i < jobs.GetNumber(); i++)

{

for (int j = 0; j < jobs.GetNumbers() && j != i; j++)

{

if (jobs.GetData(i).Equals(jobs.GetData(j)))

{

earnings = earnings + (jobs.GetData(j).Earnings() + jobs.GetData(i).Earnings());

}

}

}

return earnings;

}

static Work MaxEarnings(WorkArray jobs, MaxWork maxWork)

{

Job max = jobs.GetData(0);

for (int i = 1; i < jobs.GetNumber(); i++)

{

for (int j = 0; j < jobs.GetNumber(); j++)

{

if (jobs.GetData(i).Equals(jobs.GetData(j)))

{

maxJobs.Deti(jobs.GetData(i).GetName(), Days(jobs), Units(jobs), Earnings(jobs), jobs.GetData(i));

}

}

Console.WriteLine("{0} {1} {2} {3}", maxWork.GetName(), maxWork.GetDay(), maxWork.GetDetailQuantity(), maxWork.GetWork());

}

return max;

}

}

    }
}

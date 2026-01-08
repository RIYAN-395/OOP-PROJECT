# OOP-PROJECT
This is a comprehensive crime analysis system in C++ that evaluates and generates reports for Detective, State Crime, Cyber Crime, and Corruption cases, calculating risk/suspicion scores with detailed notes for each case.
#include <iostream>
#include <vector>
#include <string>
#include <cmath>
#include <fstream>

using namespace std;

// ===== STATE CRIME ANALYST =====
class StateCrimeAnalyst
{
private:
    int stateCrimeScore;
    string accusedName;
    string position;
    string stateDepartment;
    vector<string> notes;

public:
    void initializeScore()
    {
        stateCrimeScore = 0;
        notes.clear();
    }

    void setDetails()
    {
        cin.ignore();
        cout << "Enter Accused Name: ";
        getline(cin, accusedName);
        cout << "Enter Position: ";
        getline(cin, position);
        cout << "Enter Department: ";
        getline(cin, stateDepartment);
    }

    void checkAbuseOfPower(bool flag)
    {
        if (flag)
        {
            stateCrimeScore += 25;
            cout << "Abuse of power detected (+25)" << endl;
            notes.push_back("Abuse of power detected (+25)");
        }
    }

    void checkHumanRightsViolation(bool flag)
    {
        if (flag)
        {
            stateCrimeScore += 30;
            cout << "Human rights violation reported (+30)" << endl;
            notes.push_back("Human rights violation reported (+30)");
        }
    }

    void checkElectionFraud(bool flag)
    {
        if (flag)
        {
            stateCrimeScore += 35;
            cout << "Election fraud indicators found (+35)" << endl;
            notes.push_back("Election fraud indicators found (+35)");
        }
    }

    void checkMisuseOfPublicFunds(bool flag)
    {
        if (flag)
        {
            stateCrimeScore += 20;
            cout << "Misuse of public funds (+20)" << endl;
            notes.push_back("Misuse of public funds (+20)");
        }
    }

    void checkUnlawfulDetention(bool flag)
    {
        if (flag)
        {
            stateCrimeScore += 25;
            cout << "Unlawful detention cases (+25)" << endl;
            notes.push_back("Unlawful detention cases (+25)");
        }
    }

    void checkExcessiveForce(bool flag)
    {
        if (flag)
        {
            stateCrimeScore += 30;
            cout << "Excessive use of force reported (+30)" << endl;
            notes.push_back("Excessive use of force reported (+30)");
        }
    }

    string getName() { return accusedName; }
    string getPosition() { return position; }
    string getDepartment() { return stateDepartment; }
    int getScore() { return stateCrimeScore; }
    vector<string> getNotes() { return notes; }
};

// ===== CORRUPTION ANALYST =====
struct CorruptionCase
{
    string caseID;
    string suspectName;
    string department;
    bool foreignTransactions;
    bool anonymousTips;
    bool assetsMismatch;
    int evidenceCount;
};

class AssetModule
{
public:
    int checkAssets(bool mismatch)
    {
        if (mismatch)
        {
            cout << "Undeclared or mismatched assets found (+25)" << endl;
            return 25;
        }
        else
        {
            cout << "All assets declared properly." << endl;
            return 0;
        }
    }
};

class CorruptionAnalyst
{
private:
    int riskScore;
    vector<string> notes;

public:
    CorruptionAnalyst()
    {
        riskScore = 0;
    }

    void checkForeign(bool foreign)
    {
        if (foreign)
        {
            riskScore += 20;
            cout << "Foreign transactions found (+20)" << endl;
            notes.push_back("Foreign transactions found (+20)");
        }
    }

    void checkTips(bool tips)
    {
        if (tips)
        {
            riskScore += 20;
            cout << "Anonymous tips received (+20)" << endl;
            notes.push_back("Anonymous tips received (+20)");
        }
    }

    void checkEvidence(int count)
    {
        int score = count * 10;
        riskScore += score;
        cout << "Evidence items: " << count << " (+" << score << ")" << endl;
        notes.push_back("Evidence items: " + to_string(count) + " (+" + to_string(score) + ")");
    }

    void checkDepartment(string dept)
    {
        if (dept == "Finance" || dept == "Customs")
        {
            riskScore += 20;
            cout << "High risk department (+20)" << endl;
            notes.push_back("High risk department (+20)");
        }
    }

    void addScore(int score)
    {
        if (score > 0)
        {
            notes.push_back("Assets mismatch detected (+25)");
        }
        riskScore += score;
    }

    int getScore() { return riskScore; }
    vector<string> getNotes() { return notes; }
};

// ===== DETECTIVE MODULE =====
struct CaseData
{
    string suspectName;
    bool hasAlibi;
    vector<string> evidence;
    string witnessStatement;
    int crimeTime;
    int suspectTime;
};

class Detective
{
private:
    int suspicionScore;
    vector<string> notes;

public:
    Detective()
    {
        suspicionScore = 0;
    }

    void analyzeAlibi(bool alibi)
    {
        if (!alibi)
        {
            suspicionScore += 30;
            notes.push_back("Suspect has no alibi (+30)");
        }
    }

    void analyzeEvidence(int count)
    {
        int score = count * 10;
        suspicionScore += score;
        notes.push_back("Evidence items found: " + to_string(count) + " (+" + to_string(score) + ")");
    }

    void analyzeWitness(string statement)
    {
        if (statement != "none")
        {
            suspicionScore += 20;
            notes.push_back("Witness mentioned suspect (+20)");
        }
    }

    void analyzeTime(int crime, int suspect)
    {
        if (abs(crime - suspect) <= 1)
        {
            suspicionScore += 20;
            notes.push_back("Suspect time close to crime time (+20)");
        }
    }

    int getScore() { return suspicionScore; }
    vector<string> getNotes() { return notes; }
};

// ===== CYBER ANALYST =====
struct CyberCase
{
    string caseID;
    string caseType;
    string username;
    string ipAddress;
    bool vpnUsed;
    bool foreignIP;
    vector<string> digitalEvidence;
};

class CyberAnalyst
{
private:
    int threatScore;
    vector<string> notes;

public:
    CyberAnalyst()
    {
        threatScore = 0;
    }

    void analyzeNetwork(bool vpn, bool foreign)
    {
        if (vpn)
        {
            threatScore += 20;
            notes.push_back("VPN/Proxy detected (+20)");
        }
        if (foreign)
        {
            threatScore += 15;
            notes.push_back("Foreign IP address detected (+15)");
        }
    }

    void analyzeEvidence(int count)
    {
        int score = count * 10;
        threatScore += score;
        notes.push_back("Digital evidence count: " + to_string(count) + " (+" + to_string(score) + ")");
        if (count >= 3)
        {
            threatScore += 20;
            notes.push_back("Multiple digital evidences found (+20)");
        }
    }

    void analyzeAccount(string type)
    {
        if (type == "phishing" || type == "hacking")
        {
            threatScore += 20;
            notes.push_back("High-risk cyber crime type (+20)");
        }
    }

    int getScore() { return threatScore; }
    vector<string> getNotes() { return notes; }
};

// ===== FINAL REPORT BASE =====
class FinalReport
{
public:
    virtual void displayReport() = 0;
    virtual ~FinalReport() {}
};

class GenericFinalReport : public FinalReport
{
    string title;
    int score;
    vector<string> notes;

public:
    GenericFinalReport(string t, int s, vector<string> n)
    {
        title = t;
        score = s;
        notes = n;
    }

    void displayReport() override
    {
        cout << "\n===== " << title << " =====" << endl;
        cout << "Score: " << score << endl;
        cout << "Notes:" << endl;
        for (auto& n : notes)
        {
            cout << "- " << n << endl;
        }
        cout << "=============================" << endl;
    }
};

// ===== MAIN =====
int main()
{
    vector<FinalReport*> allReports;
    int mainChoice;

    while (true)
    {
        system("cls");
        cout << "===== CRIME ANALYSIS SYSTEM =====" << endl;
        cout << "1. Detective Case" << endl;
        cout << "2. State Level Crime" << endl;
        cout << "3. Cyber Crime" << endl;
        cout << "4. Corruption Case" << endl;
        cout << "5. Exit" << endl;
        cout << "Enter your choice: ";
        cin >> mainChoice;

        if (mainChoice == 1)
        {
            CaseData data;
            cin.ignore();

            cout << "Enter suspect name: ";
            getline(cin, data.suspectName);

            char al;
            cout << "Does suspect have alibi (y/n): ";
            cin >> al;
            data.hasAlibi = (al == 'y' || al == 'Y');

            int n;
            cout << "Number of evidence items: ";
            cin >> n;
            cin.ignore();

            for (int i = 0; i < n; i++)
            {
                string e;
                cout << "Enter evidence " << i + 1 << ": ";
                getline(cin, e);
                data.evidence.push_back(e);
            }

            cout << "Witness statement (type 'none' if no witness): ";
            getline(cin, data.witnessStatement);

            cout << "Crime time (0-23): ";
            cin >> data.crimeTime;
            cout << "Suspect time (0-23): ";
            cin >> data.suspectTime;

            Detective d;
            d.analyzeAlibi(data.hasAlibi);
            d.analyzeEvidence(data.evidence.size());
            d.analyzeWitness(data.witnessStatement);
            d.analyzeTime(data.crimeTime, data.suspectTime);

            allReports.push_back(
                new GenericFinalReport("FINAL DETECTIVE REPORT", d.getScore(), d.getNotes())
            );

            system("pause");
        }
        else if (mainChoice == 2)
        {
            StateCrimeAnalyst sc;
            sc.initializeScore();
            sc.setDetails();

            int choice;
            cout << "Abuse of Power? ";
            cin >> choice;
            sc.checkAbuseOfPower(choice);

            cout << "Human Rights Violation? ";
            cin >> choice;
            sc.checkHumanRightsViolation(choice);

            cout << "Election Fraud? ";
            cin >> choice;
            sc.checkElectionFraud(choice);

            cout << "Misuse of Public Funds? ";
            cin >> choice;
            sc.checkMisuseOfPublicFunds(choice);

            cout << "Unlawful Detention? ";
            cin >> choice;
            sc.checkUnlawfulDetention(choice);

            cout << "Excessive Use of Force? ";
            cin >> choice;
            sc.checkExcessiveForce(choice);

            allReports.push_back(
                new GenericFinalReport("FINAL STATE CRIME REPORT", sc.getScore(), sc.getNotes())
            );

            system("pause");
        }
        else if (mainChoice == 3)
        {
            CyberCase c;
            cin.ignore();

            cout << "Enter Case ID: ";
            getline(cin, c.caseID);

            cout << "Enter Case Type (hacking/phishing/fraud): ";
            getline(cin, c.caseType);

            cout << "Enter suspect username/email: ";
            getline(cin, c.username);

            cout << "Enter IP address: ";
            getline(cin, c.ipAddress);

            char ch;
            cout << "Was VPN used (y/n): ";
            cin >> ch;
            c.vpnUsed = (ch == 'y' || ch == 'Y');

            cout << "Is IP foreign (y/n): ";
            cin >> ch;
            c.foreignIP = (ch == 'y' || ch == 'Y');

            int n;
            cout << "Number of digital evidence items: ";
            cin >> n;
            cin.ignore();

            for (int i = 0; i < n; i++)
            {
                string e;
                cout << "Enter evidence " << i + 1 << ": ";
                getline(cin, e);
                c.digitalEvidence.push_back(e);
            }

            CyberAnalyst analyst;
            analyst.analyzeNetwork(c.vpnUsed, c.foreignIP);
            analyst.analyzeEvidence(c.digitalEvidence.size());
            analyst.analyzeAccount(c.caseType);

            allReports.push_back(
                new GenericFinalReport("FINAL CYBER REPORT", analyst.getScore(), analyst.getNotes())
            );

            system("pause");
        }
        else if (mainChoice == 4)
        {
            CorruptionCase c;
            cin.ignore();

            cout << "Enter Case ID: ";
            getline(cin, c.caseID);

            cout << "Enter Suspect Name: ";
            getline(cin, c.suspectName);

            cout << "Enter Department: ";
            getline(cin, c.department);

            char ch;
            cout << "Foreign transactions? (y/n): ";
            cin >> ch;
            c.foreignTransactions = (ch == 'y' || ch == 'Y');

            cout << "Anonymous tips? (y/n): ";
            cin >> ch;
            c.anonymousTips = (ch == 'y' || ch == 'Y');

            cout << "Assets mismatch? (y/n): ";
            cin >> ch;
            c.assetsMismatch = (ch == 'y' || ch == 'Y');

            cout << "Number of evidence items: ";
            cin >> c.evidenceCount;

            CorruptionAnalyst analyst;
            AssetModule asset;

            analyst.checkForeign(c.foreignTransactions);
            analyst.checkTips(c.anonymousTips);
            analyst.checkEvidence(c.evidenceCount);
            analyst.checkDepartment(c.department);
            analyst.addScore(asset.checkAssets(c.assetsMismatch));

            allReports.push_back(
                new GenericFinalReport("FINAL CORRUPTION REPORT", analyst.getScore(), analyst.getNotes())
            );

            system("pause");
        }
        else if (mainChoice == 5)
        {
            system("cls");
            cout << "===== FINAL REPORT SUMMARY =====" << endl;

            for (auto& r : allReports)
            {
                r->displayReport();
                delete r;
            }
            return 0;
        }
        else
        {
            cout << "Invalid choice! Please try again." << endl;
            system("pause");
        }
    }
}

#include<iostream>
#include<cstring>
using namespace std;

struct Student {
    int rollno;
    char name[30];
    float sgpa;
};

void display(struct Student s[], int n);
void bubblesort(struct Student s[], int n);
void insertionsort(struct Student s[], int n);
void binarysearch(struct Student s[],int n,char data[]);
int main() {
    struct Student s[30];
    int i, ch, n;
    char na[30];
    cout << "\nEnter number of students: ";
    cin >> n;
    cout << "\nEnter the information of students:";

    for(i = 0; i < n; i++) {
        cout << "\nEnter the rollno, name, sgpa: ";
        cin >> s[i].rollno >> s[i].name >> s[i].sgpa;
    }
    display(s, n);

    do {
        cout << "\n1.Bubble Sort";
        cout << "\n2.Insertion Sort";
        cout<<"\n3.Binary Sort";
        cout << "\n4. Exit";
        cin >> ch;

        switch(ch) {
            case 1:
                bubblesort(s, n);
                break;
            case 2:
                insertionsort(s, n);
                break;
            case 3:cout<<"\nEnter the name to search";
                cin>>na;
                binarysearch(s,n,na);
                break;
            case 4:
                 break;
            default:
                cout << "Invalid choice. Please try again.";
        }
    } while(ch != 4);

    return 0;
}

void display(struct Student s[30], int n) {
    cout << "\nRollno\tName\tSGPA";
    for(int i = 0; i < n; i++) {
        cout << "\n" << s[i].rollno << "\t" << s[i].name << "\t" << s[i].sgpa;
    }
}

void bubblesort(struct Student s[30], int n) {
    int temp, i, j;
    char na[30];
    float sg;

    for(i = 0; i < n-1; i++) { // Outer loop should go up to n-1
        for(j = 0; j < n-i-1; j++) { // Inner loop should compare up to n-i-1
            if(s[j].rollno > s[j+1].rollno) {
                // Swap rollno
                temp = s[j].rollno;
                s[j].rollno = s[j+1].rollno;
                s[j+1].rollno = temp;
                
                // Swap sgpa
                sg = s[j].sgpa;
                s[j].sgpa = s[j+1].sgpa;
                s[j+1].sgpa = sg;
                
                // Swap name
                strcpy(na, s[j].name);
                strcpy(s[j].name, s[j+1].name);
                strcpy(s[j+1].name, na);
            }
        }
    }
    cout << "\nThe sorted data by rollno is:\n";
    display(s, n);
}

void insertionsort(struct Student s[30], int n) {
    int i, j, r;
    float sg;
    char na[30];

    for(i = 1; i < n; i++) {
        strcpy(na, s[i].name);
        r = s[i].rollno;
        sg = s[i].sgpa;
        
        j=i-1;
        while(j >= 0 && strcmp(s[j].name, na) > 0) {
            strcpy(s[j+1].name, s[j].name);
            s[j+1].rollno=s[j].rollno;
            s[j+1].sgpa=s[j].sgpa;
            j--;
        }
        strcpy(s[j+1].name, na);
        s[j+1].rollno=r;
        s[j+1].sgpa=sg;
    }
    cout << "\nSorted data according to Name:\n";
    display(s, n);
}
void binarysearch(struct Student s[],int n,char data[]){
    int left=0,right=n-1,mid,flag=0;
    while(left<=right){
        mid=(left+right)/2;
        if(strcmp(data,s[mid].name)==0)
        {
            flag=1;
            break;
        }
        else if(strcmp(data,s[mid].name)<0)
        {
            right=mid-1;
        }
        else
        {
            right=mid+1;
        }
    }
    if(flag==1)
    {
        cout<<"\nRollNo="<<s[mid].rollno;
        cout<<"\nName="<<s[mid].name;
        cout<<"\nSGPA="<<s[mid].sgpa;
    }
    else
    {
        cout<<"\n Data not found";
    }
    }


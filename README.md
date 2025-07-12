smart-railway-ticket-system-code-using-c-language
#include<iostream>
#include<conio.h>
using namespace std;
struct train{
    int trainid;
    char name[50];
    char source[50];
    char destination[30];
    char time[60];
    int fareperkm;
};
struct ticket{
    int ticketid;
    char name[60];
    int age;
    int distance;
    int classtype;
    int fare;
    int valid;
    
};
train trains[50];
ticket tickets[1000];
int traincount =0;
int ticketcount = 0;
int sleeperfare = 5;
int ac3tier =7;
int acfirst = 10;
int sleeperseat=1;
int ac3tierseat =1;
int acfirstseat = 1;
int reservedseat= 0;
int reservedfare = 2;
void addtrain(){
    char choice;
   do{
    if(traincount>= 10 ){
        cout<<"no more trains can be added\n ";
        break;
    }
    cout<<"Enter train id of the train you want to add : ";
    cin>>trains[traincount].trainid;
    cout<<"Enter train name(eg.Rajdhani etc) : ";
    cin>>trains[traincount].name;
    cout<<"Enter source(from where train begins) :";
    cin>>trains[traincount].source;
    cout<<"Enter destination(where it will reach) :";
    cin>>trains[traincount].destination;
    cout<<"Enter time :";
    cin>>trains[traincount].time;
    cout<<"Enter fareperkm :";
    cin>>trains[traincount].fareperkm;
    cout<<"TRAIN DATA ADDED SUCCESFULLY\n";
    traincount++;
    cout<<"Wanted to add another train ? : ";
    cin>>choice;
   }while(choice =='y' || choice == 'Y');
}
void listtrain(){ 
    if(traincount == 0){
        cout<<"there is no train data added yet";
        return ;
    }
    else{
    cout<<"\n------ AVAILABLE TRAINS----\n";
    for(int i = 0;i<traincount;i++){
        cout<<"TRAINID :"<<trains[i].trainid<<"\nNAME   :"<<trains[i].name<<"\nSOURCE :"<<trains[i].source<<"\nDESTINATION :"<<trains[i].destination<<"\nTIME   :"<<trains[i].time<<"\nFAREPERKM  :"<<trains[i].fareperkm<<endl;
    }
}}
void bookticket(){
    if(traincount == 0 ){
        cout<<"no available trains to book";
        return;
    }
    int trainid1;
    char choice;
    do{
         int found = -1;
         int trainid1;
    
    cout<<"\nenter train id you want to book ticket";
    cin>>trainid1;
    for(int i = 0;i<traincount;i++){
        if(trains[i].trainid== trainid1)
        {
            found = i;
            break;}
        }
            if(found == -1){
                cout<<"INVALID TRAIN";
            }
            else {
            cout<<"Enter ticketid: ";
            cin>>tickets[ticketcount].ticketid;
         
            cout<<"Enter passenger name : ";
            cin>>tickets[ticketcount].name;
            cout<<"Enter passenger age : ";
            cin>>tickets[ticketcount].age;
            cout<<"Enter distance : ";
            cin>>tickets[ticketcount].distance;
            cout << "\nClass Options:\n";
            cout << "1. Sleeper (x1)\n";
            cout << "2. AC 3-tier (x2)\n";
            cout << "3. AC First (x3)\n";
            cout << "4. Reserved (x4)\n";

            cout<<"Enter  class no from above options : ";
            cin>>tickets[ticketcount].classtype;
            if(tickets[ticketcount].classtype == 1 ){
            tickets[ticketcount].fare = trains[found].fareperkm*tickets[ticketcount].distance*sleeperfare;
            cout<<"\nTicket fare : "<<tickets[ticketcount].fare;
        }
        else if(tickets[ticketcount].classtype == 2 ){
            tickets[ticketcount].fare = trains[found].fareperkm*tickets[ticketcount].distance*ac3tier;
            cout<<"\nTicket fare : "<<tickets[ticketcount].fare;
        }
        else if(tickets[ticketcount].classtype == 3){
            tickets[ticketcount].fare = trains[found].fareperkm*tickets[ticketcount].distance*acfirst;
            cout<<"\nTicket fare : "<<tickets[ticketcount].fare;
        }
        else if(tickets[ticketcount].classtype == 4){
            tickets[ticketcount].fare = trains[found].fareperkm*tickets[ticketcount].distance*reservedfare;
            cout<<"\nTicket fare : "<<tickets[ticketcount].fare;
        }
        cout << "\n Ticket Booked:\n";
        cout<<"\nTicket id : "<<tickets[ticketcount].ticketid;
         cout<<"\nTrain id : "<<trains[found].trainid;
        cout<<"\nPassenger Name :"<<tickets[ticketcount].name;
         cout<<"\nPassenger age  : "<<tickets[ticketcount].age;
         cout<<"\nSource : "<<trains[found].source;
         cout<<"\nDestination : "<<trains[found].destination;
        if(tickets[ticketcount].classtype ==1){
            cout<<"\nTicket class type : sleeper";
            cout<<"\ncoach : A1";
             cout<<"\nSeat :  "<<sleeperseat;
             sleeperseat++;
        }
        else if(tickets[ticketcount].classtype ==2){
            cout<<"\nTicket class type : AC 3-tier";
             cout<<"\ncoach : A2";
              cout<<"\nSeat :  "<<ac3tierseat;
             ac3tierseat++;
        }
        else  if(tickets[ticketcount].classtype ==3){
            cout<<"\nTicket class type : AC first";
             cout<<"\ncoach : A3";
             cout<<"\nSeat :  "<<acfirstseat;
             acfirstseat++;
        }
        else  if(tickets[ticketcount].classtype ==4){
            cout<<"\nTicket class type : Reserved";
             cout<<"\ncoach : A4";
             cout<<"\nSeat :  "<<reservedseat;
             reservedseat++;

        cout<<"\nPassenger Fare :"<<tickets[ticketcount].fare;
        tickets[ticketcount].valid = 1;
        ticketcount++;
    cout<<"\nWanted one more ticket ? : ";
    cin>>choice;
}
   }}while(choice =='y' || choice == 'Y');}
void cancelticket(){
    if(ticketcount == 0){
        cout<<"NO TICKETS BOOKED YET ";
    }
    int cancelid;
    cout<<"enter ticket id you want to cancel";
    cin>>cancelid;
    for(int i = 0;i<ticketcount;i++){
        if(tickets[i].ticketid == cancelid && tickets[i].valid == 1 ){
            tickets[i].valid == 0 ;
             cout << "Ticket with ID " << cancelid << " has been cancelled.\n";
             break;
        }
         else  {
        cout << "Ticket ID not found or already cancelled.\n";
    }
    }
}
main() {
    int option;
    addtrain();
    do {
        cout << "\n--- Railway Ticket System ---\n";
        cout << "1. Add Train\n";
        cout << "2. List Trains\n";
        cout << "3. Book Ticket\n";
        cout << "4. Cancel Ticket\n";
        cout << "5. Exit\n";
        cout << "Enter your option: ";
        cin >> option;
        switch(option) {
            case 1: addtrain(); break;
            case 2: listtrain(); break;
            case 3: bookticket(); break;
            case 4: cancelticket(); break;
            case 5: cout << "Exiting program.\n"; break;
            default: cout << "Invalid option.\n";
        }
    } while(option != 5);   
}

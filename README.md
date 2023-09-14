# August26Task

 Two task all needs to perform as tomorrow is working Saturday.  In your personal dev org.  
** TASK 1:  **
 Create a Custom field on Contact IsActive__c of type checkbox 
 Create a Custom field of Number type on Account NumberOfActiveContact__c on Account  
 Create a Custom Checkbox on Account SkipContactCascadeDelete__c   
 Part 1: Number of Active Contacts should be rolled up to Account. If an account has 10 contacts out of which 6 are active and 4 inactive then 6 should be rolled up to Account If I update one Contact to InActive then the count should be 5 and If I delete one Active Contact then the count should be 4 Now If I delete 1 inactive Contact then count should remain 4  
 
 Part 2: If I delete an Account then all its related Contacts should be deleted. If SkipContactCascadeDelete__c is true then no contact should be deleted when I delete the Account.   In the above trigger user proper names of variables, the Handler class.  

 public class HAndlerAccountTriggerCon {
        public static void preventDeleteOnAccount(List<Account> accountsToDelete) {	
        Set<Id> accId = new Set<Id>();
    	for(Account acc : accountsToDelete){
        if(acc.SkipContactCascadeDelete__c){
            accId.add(acc.id);
        }
       
    }
    
    List<Contact> contactUpdate = [SELECT ID,AccountId from contact where id in:accId];
    List<Contact> contact = new List<contact>();
    for(Contact con : contactUpdate){
        con.AccountId = null;
    	contact.add(con);
    }
    
    if(!contact.isEmpty()){
    update contact;
        }
            
     }

}

trigger AccountTriggerCon on Account (Before delete) {
     HAndlerAccountTriggerCon.preventDeleteOnAccount(Trigger.old);
}

 
 **TASK 2 : **
 Create an LWC component that will display all the Objects and on the selection of objects, it will display all the fields in multi multi-select box.  Then I will be able to Query all the records of the Selected Fields and Objects.  Wireframe of the LWC task:  https://drive.google.com/file/d/1WIWg5paAvlHMX0gjs4h1LciO9jS7Ok8B/view?usp=sharing  In the above there will be a total of four LWC Component 1. Main.html which will contain all the buttons. 2. Picklist.html 3. Multipicklist.html (https://niksdeveloper.com/salesforce/multi-select-picklist-in-lwc-using-lightning-dual-listbox/#:~:text=To%20use%20a%20multi%2Dselect%20picklist%20in%20LWC%2C%20we%20need,get%20the%20Record%20Type%20details.) 4. Table.HTML  In above Picklist, Multipicklist, and Table should not contain any button, Button, and events should be handled via only Main.html and all will communicate via parent-child events, LMS and API variables.  All will perform the above task and send me a video recoding of the code explanation and demo to me on my email. Apex class should be named as Util.cls

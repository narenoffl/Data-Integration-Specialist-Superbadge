@RestResource(urlMapping='/project/*')
global with sharing class ProjectRESTService {
  @HttpPost
  global static String postProjectData(String ProjectRef, String ProjectName, String OpportunityId, Date StartDate, Date EndDate, Double Amount, String Status) {
      List<Project__c> projects = [SELECT Billable_Amount__c,End_Date__c,Id,Name,Opportunity__c,ProjectRef__c,Start_Date__c,Status__c FROM Project__c WHERE ProjectRef__c = :ProjectRef];
      Project__c project = new Project__c();
      if(projects.size() > 0)
          project = projects.get(0);
      
      Savepoint sp = Database.setSavepoint();
      try{
          project.Billable_Amount__c = Amount;
          project.End_Date__c = EndDate;
          project.Name = ProjectName;
          project.Opportunity__c = OpportunityId;
          project.ProjectRef__c = ProjectRef;
          project.Start_Date__c = StartDate;
          project.Status__c = Status;
          upsert project;
          
          //Update Opportunity
          Opportunity opportunity = [SELECT Id, DeliveryInstallationStatus__c FROM Opportunity WHERE Id = :OpportunityId];
          opportunity.DeliveryInstallationStatus__c = 'In progress';
          update opportunity;
          
          return 'OK';
      }
      catch(exception ex){
          Database.rollback(sp);
          return ex.getMessage();
      }
   }
}


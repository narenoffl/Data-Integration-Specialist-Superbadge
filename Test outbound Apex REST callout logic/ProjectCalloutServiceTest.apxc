@isTest
private class ProjectCalloutServiceTest {
  //Implement mock callout tests here
   @testSetup static void testSetupdata(){
        //create the opportunity record
        Opportunity opp1 = new Opportunity();
        opp1.Name = 'Test Opp1';
        opp1.Type = 'New Project';
        opp1.Amount = 100;
        opp1.CloseDate = Date.today();
        opp1.StageName = 'Submitted Project';
        insert opp1;
        //create the opportunity record
        Opportunity opp2 = new Opportunity();
        opp2.Name = 'Test Opp2';
        opp2.Type = 'New Project';
        opp2.Amount = 200;
        opp2.CloseDate = Date.today();
        opp2.StageName = 'Resubmit Project';
        insert opp2;
        //create the Custom Settings
        ServiceTokens__c servToken = new ServiceTokens__c();
        servToken.Name = 'ProjectServiceToken';
        servToken.Token__c = 'qwertyuiopnjhgft';
        insert servToken;
    }
  
  @isTest
  static void testSuccessMessage(){
      Opportunity opp = [Select Id, Name FROM Opportunity WHERE Name = 'Test Opp1' Limit 1];
      List<Id> lstOfOppIds = new List<Id>();
      lstOfOppIds.add(opp.Id);
      // Set mock callout class
      Test.setMock(HttpCalloutMock.class, new ProjectCalloutServiceMock());
      // This causes a fake response to be sent
      // from the class that implements HttpCalloutMock. 
      Test.startTest();
          ProjectCalloutService.postOpportunityToPMS(lstOfOppIds);
      Test.stopTest();    
      // Verify that the response received contains fake values        
      opp = [select StageName from Opportunity where id =: opp.Id];
      System.assertEquals('Submitted Project',opp.StageName);     
  }
  
  @isTest
  static void testFailureMessage(){
      Opportunity opp = [Select Id, Name FROM Opportunity WHERE Name = 'Test Opp2' Limit 1];
      List<Id> lstOfOppIds = new List<Id>();
      lstOfOppIds.add(opp.Id);
      // Set mock callout class
      Test.setMock(HttpCalloutMock.class, new ProjectCalloutServiceMockFailure());
      // This causes a fake response to be sent
      // from the class that implements HttpCalloutMock. 
      Test.startTest();
          ProjectCalloutService.postOpportunityToPMS(lstOfOppIds);
      Test.stopTest();    
      // Verify that the response received contains fake values        
      opp = [select StageName from Opportunity where id =: opp.Id];
      System.assertEquals('Resubmit Project',opp.StageName);
  }
}
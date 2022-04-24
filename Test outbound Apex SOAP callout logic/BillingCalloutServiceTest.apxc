@isTest
private class BillingCalloutServiceTest {
  @testSetup static void loadData(){
        
        Opportunity oppo = new Opportunity();
        oppo.Name = 'TestOpp1';
        oppo.CloseDate = Date.today();
        oppo.StageName = 'Prospecting';
        insert oppo;
        
        Project__c proj = new Project__c();
        proj.Name = 'TestProj1';
        proj.Billable_Amount__c = 1000;        
        proj.ProjectRef__c = 'TestRef1';
        proj.Status__c = 'Running';
        proj.Opportunity__c = oppo.Id;
        insert proj;
        
        ServiceCredentials__c servCred = new ServiceCredentials__c();
        servCred.Name = 'BillingServiceCredential';
        servCred.Username__c = 'usr1';
        servCred.Password__c = 'pwd1';
        insert servCred;
    }
    
    @isTest static void testCalloutSuccess(){
        Test.setMock(WebServiceMock.class, new BillingCalloutServiceMock()); 
        List<Project__c> prjt = [SELECT Status__C FROM Project__c WHERE ProjectRef__c = 'TestRef1'];
        System.assertEquals(1, prjt.size());
        Test.startTest(); 
            prjt[0].Status__c = 'Billable';
            update prjt;
        Test.stopTest();
    }
    
    @isTest static void testCalloutFailure(){
        Test.setMock(WebServiceMock.class, new BillingCalloutServiceMockFailure()); 
        List<Project__c> prjt = [SELECT Status__C FROM Project__c WHERE ProjectRef__c = 'TestRef1'];
        System.assertEquals(1, prjt.size());
        Test.startTest(); 
            prjt[0].Status__c = 'Running';
            update prjt;
        Test.stopTest();
    }
}
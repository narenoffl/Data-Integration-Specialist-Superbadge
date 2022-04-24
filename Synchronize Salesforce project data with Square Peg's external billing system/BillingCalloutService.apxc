public class BillingCalloutService {
    @future(callout = true)
    public static void callBillingService(String projectRef, Decimal billingAmount){
        ServiceCredentials__c srvcCrd = ServiceCredentials__c.getValues('BillingServiceCredential');
                
        BillingServiceProxy.project projectInst = new BillingServiceProxy.project();
        projectInst.username = srvcCrd.Username__c;
        projectInst.password = srvcCrd.Password__c;
        projectInst.billAmount = billingAmount;
        
        BillingServiceProxy.InvoicesPortSoap11 invPortSoapInst = new BillingServiceProxy.InvoicesPortSoap11();
        String response = invPortSoapInst.billProject(projectInst);
        
        List<Project__c> lstOfProjects = new List<Project__c>();
        if(response != null && response.equalsIgnoreCase('OK')){
            List<Project__c> lstOfPrjts = [SELECT Status__c FROM Project__c WHERE ProjectRef__c = :projectRef];
            for(Project__c prjt : lstOfPrjts){
                prjt.Status__c = 'Billed';
                
                lstOfProjects.add(prjt);
            }
            
            UPDATE lstOfProjects;
        }
    }
}
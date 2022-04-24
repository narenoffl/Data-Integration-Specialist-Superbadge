trigger ProjectTrigger on Project__c (after update) {
    if(Trigger.isAfter && Trigger.isUpdate){
        for(Project__c prjt : Trigger.new){
            if(prjt.Status__c != null && prjt.Status__c.equals('Billable')){
                BillingCalloutService.callBillingService(prjt.ProjectRef__c, prjt.Billable_Amount__c);
            }
        }
    }
}
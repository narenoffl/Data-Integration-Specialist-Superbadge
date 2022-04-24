@isTest
global class ProjectCalloutServiceMockFailure implements HttpCalloutMock{
   //Implement http mock callout here
   // Implement this interface method
   global HTTPResponse respond(HTTPRequest request){
       // Create a fake response
       HttpResponse response = new HttpResponse();
       response.setHeader('Content-Type', 'application/json');
       response.setStatus('Bad Response');
       response.setStatusCode(500);
              
       return response;
   }
}
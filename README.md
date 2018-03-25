# REST-Template

Easy way to use REST-Template in Spring-Boot application to Consume Webservice with Basic authentication.


Steps:
 1. Declare RestTemplate ---> RestTemplate restTemplate = new RestTemplate();
 2. Create ResponseEntity ---> ResponseEntity<ResponseList> response;
 3. Create HttpHeaders ---> HttpHeaders headers = new HttpHeaders();
 4. Now set contentType, Authorization --->
 
      headers.setContentType(MediaType.APPLICATION_JSON);
      headers.add("Accept", "application/json");
      headers.set("Authorization","Basic " + new String(Base64.encodeBase64(userAndPass.getBytes(Charset.forName("US-ASCII"))))); 
      
      *userAndPass is what you have declare as username and password (eg: String userAndPass = "xyz:xyz123";)
 
 5. Create HttpEntity ---> HttpEntity<String> requestEntity = new HttpEntity<>("Headers", headers);
 6. Call webservice using RestTemplate ---> response = this.restTemplate.exchange(url, HttpMethod.GET, requestEntity, ResponseList.class);  
 7. Get responseBody ---> ResponseList responseList = response.getBody();


 *ResponseList -> It is a POJO class where you have structured your response according to the JSON response from webservice.
 
 "This is how you can enjoy consuming Webservice in Spring-boot application using Rest-Template."
 
 
 *Code Snippet for REST-Template example:
 
	public List<TO> consumeWS() {

		RestTemplate restTemplate = new RestTemplate();
		ResponseEntity<ResponseList> response;
		String userAndPass = "xyz:xyz123";
		HttpHeaders headers = new HttpHeaders();
		headers.setContentType(MediaType.APPLICATION_JSON);
		headers.add("Accept", "application/json");
		headers.set("Authorization","Basic " + new String(Base64.encodeBase64(userAndPass.getBytes(Charset.forName("US-ASCII")))));
		String url = "http://xyz-007-machine.com";
		HttpEntity<String> requestEntity = new HttpEntity<>("Headers", headers);
		response = this.restTemplate.exchange(url, HttpMethod.GET, requestEntity, ResponseList.class);
		List<TO> webserviceLst = new ArrayList<>();
		ResponseList responseLst = response.getBody();
		webserviceLst = responseLst.getResponseList();
		return webserviceLst;

	}
  
  
  
  
   
 *Upload, Download, HTTPS calls will be in the next articles :)
 

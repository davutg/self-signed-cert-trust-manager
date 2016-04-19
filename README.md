# self-signed-cert-trust-manager
Automatically exported from code.google.com/p/self-signed-cert-trust-manager


Some ways to omit SSL certificate validation

1)
	CustomTrustManager.initSsl();
	
2)
	AxisProperties.setProperty("axis.socketSecureFactory","org.apache.axis.components.net.SunFakeTrustSocketFactory");
	
3)	
// Create a trust manager that does not validate certificate chains
//    	TrustManager[] trustAllCerts = new TrustManager[]{
//    	    new X509TrustManager() {
//    	        public java.security.cert.X509Certificate[] getAcceptedIssuers() {
//    	            return null;
//    	        }
//    	        public void checkClientTrusted(
//    	            java.security.cert.X509Certificate[] certs, String authType) {
//    	        }
//    	        public void checkServerTrusted(
//    	            java.security.cert.X509Certificate[] certs, String authType) {
//    	        }
//    	    }
//    	};
//
//    	// Install the all-trusting trust manager
//    	try {
//    	    SSLContext sc = SSLContext.getInstance("SSL");
//    	    sc.init(null, trustAllCerts, new java.security.SecureRandom());
//    	    HttpsURLConnection.setDefaultSSLSocketFactory(sc.getSocketFactory());
//    	} catch (Exception e) {
//    	}
//
//    	// Now you can access an https URL without having the certificate in the truststore
//    	try {
//    	    URL url = new URL("https://op.sagliknet.saglik.gov.tr/onlineprotokol.asmx");
//    	} catch (MalformedURLException e) {
//    		e.printStackTrace();
//    	}



Overriding MIME HEADERS for Axis 1.X in ServiceLocator



@Override
    public Call createCall() throws ServiceException {
    	 _call = new org.apache.axis.client.Call(this) {

    	        @Override
    	        public void setRequestMessage(Message msg) {
    	            MimeHeaders hd = msg.getMimeHeaders();
    	            //MimeHeaders hd = msgContext.getMessage().getMimeHeaders();
    	            hd.addHeader("Accept-Encoding","gzip,deflate");
    	            hd.addHeader("Content-Type","text/xml;charset=UTF-8");
    	            hd.addHeader("SOAPAction","http://tempuri.org/Action");
    	            hd.addHeader("Connection","Keep-Alive");

    	            super.setRequestMessage(msg);
    	        }

    	    };

    	    return _call;
    }

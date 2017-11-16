---
layout: post
title:  "Add Google reCAPTCHA to Your Website"
date:   2017-08-18
author: yuci
category: security
---

[Google reCAPTCHA][1] is a free service that protects your site from spam and abuse.

You can just follow the steps below to add it to your website.

First of all, go to [Google reCAPTCHA][2], and register your application there. Then you can work on the client and server sides respectively as below:

## On the client side ([see ref][3]) ##

First, paste the snippet below `<script...></script>` before the closing </head> tag on your HTML template, for example:

{% highlight html %}
    <script src='https://www.google.com/recaptcha/api.js'></script>
</head>
{% endhighlight %} 
Then paste the snippet below `<div...></div>` at the end of the <form> where you want the reCAPTCHA widget to appear, for example:

{% highlight html %}
    <div class="g-recaptcha" data-sitekey="{your public site key given by Google reCAPTCHA}"></div>
</form>
{% endhighlight %} 
That's all on the client side.

## On the server side ([see ref][4]) ##

When a user submits the form, you need to get the user response token from the `g-recaptcha-response` POST parameter. Then use the token, together with the secret key given by Google reCAPTCHA, and optional with the user's IP address, and then POST a request to the Google reCAPTCHA API. You'll then get the response from Google reCAPTHA, indicating whether the form verification succeeds or fails.

Below is the sample code on the server side.

 - User summits a Wicket form (Wicket 6 in this example):

{% highlight java %}
protected void onSubmit() {
    HttpServletRequest httpServletRequest = (HttpServletRequest)getRequest().getContainerRequest();
    boolean isValidRecaptcha = ReCaptchaV2.getInstance().verify(httpServletRequest);
    if(!isValidRecaptcha){
        verificationFailedFeedbackPanel.setVisible(true);
        return;
    }
    // reCAPTCHA verification succeeded, carry on handling form submission
    ...
}
{% endhighlight %}    

ReCaptchaV2.java (Just Java, web framework independent)

{% highlight java %}
import javax.servlet.http.HttpServletRequest;    
import org.apache.log4j.Logger;
import org.codehaus.jackson.map.ObjectMapper;
import org.springframework.http.HttpEntity;
import org.springframework.http.HttpHeaders;
import org.springframework.http.HttpMethod;
import org.springframework.http.MediaType;
import org.springframework.http.ResponseEntity;
import org.springframework.util.LinkedMultiValueMap;
import org.springframework.util.MultiValueMap;
import org.springframework.web.client.RestTemplate;
public class ReCaptchaV2 {
    private final static Logger logger = Logger.getLogger(ReCaptchaV2.class);
    private final static String VERIFICATION_URL = "https://www.google.com/recaptcha/api/siteverify";
    private final static String SECRET = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";
    private static ReCaptchaV2 instance = new ReCaptchaV2();
    private ReCaptchaV2() {}
    public static ReCaptchaV2 getInstance() {
        return instance;
    }
    private boolean verify(String recaptchaUserResponse, String remoteip) {
        boolean ret = false;
        if (recaptchaUserResponse == null) {
            return ret;
        }
        RestTemplate rt = new RestTemplate();
        HttpHeaders headers = new HttpHeaders();
        headers.setContentType(MediaType.APPLICATION_FORM_URLENCODED);
        MultiValueMap<String, String> map= new LinkedMultiValueMap<String, String>();
        map.add("secret", SECRET);
        map.add("response", recaptchaUserResponse);
        if (remoteip != null) {
            map.add("remoteip", remoteip);
        }
        HttpEntity<MultiValueMap<String, String>> httpEntity = new HttpEntity<MultiValueMap<String, String>>(map, headers);
        ResponseEntity<String> res = null;
        try {
            res = rt.exchange(VERIFICATION_URL, HttpMethod.POST, httpEntity, String.class);
        } catch (Exception e) {
            logger.error("Exception: " + e.getMessage());
        }
        if (res == null || res.getBody() == null) {
            return ret;
        }
        Response response = null;
        try {
            response = new ObjectMapper().readValue(res.getBody(), Response.class);
        } catch (Exception e) {
            logger.error("Exception: " + e.getMessage());
        }
        if (response != null && response.isSuccess()) {
            ret = true;
        }
        logger.info("Verification result: " + ret);
        return ret;
    }
    public boolean verify(HttpServletRequest httpServletRequest) {
        boolean ret = false;
        if (httpServletRequest == null) {
            return ret;
        }
        String recaptchaUserResponse = httpServletRequest.getParameter("g-recaptcha-response");
        String remoteAddr = httpServletRequest.getRemoteAddr();
        return verify(recaptchaUserResponse, remoteAddr);
    }
}
{% endhighlight %} 

Response.java (Java POJO)

{% highlight java %}
public class Response {
    private String challenge_ts;
    private String hostname;
    private boolean success;
    public Response() {}
    public String getChallenge_ts() {
        return challenge_ts;
    }
    public void setChallenge_ts(String challenge_ts) {
        this.challenge_ts = challenge_ts;
    }
    public String getHostname() {
        return hostname;
    }
    public void setHostname(String hostname) {
        this.hostname = hostname;
    }
    public boolean isSuccess() {
        return success;
    }
    public void setSuccess(boolean success) {
        this.success = success;
    }
    @Override
    public String toString() {
        return "ClassPojo [challenge_ts = " + challenge_ts + ", hostname = " + hostname + ", success = " + success + "]";
    }
}
{% endhighlight %} 

  [1]: https://developers.google.com/recaptcha/docs/versions
  [2]: https://www.google.com/recaptcha/admin
  [3]: https://developers.google.com/recaptcha/docs/display
  [4]: https://developers.google.com/recaptcha/docs/verify

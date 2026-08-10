# CCDL Readme
This is CCD lab Readme

## LAB 1 To Remember

### Workflow Steps
* Resolve address/name
* Create web root
* Create webpage/application
* Create server block
* Enable configuration
* Test Nginx configuration
* Reload Nginx
* Verify using browser/curl
* Inspect logs

---

### Key Concepts & Rules
* **Static Content:** Nginx serves directly.
* **PHP Content:** Nginx uses FastCGI and PHP-FPM.
* **JSP Content:** Nginx uses reverse proxy and Tomcat.
* **Testing:** Always run `nginx -t` before reloading.
* **Logs:** 
  * **Access log:** Records requests
  * **Error log:** Records failures
* **Lab Ports:**
  * **Nginx:** `8080`
  * **Tomcat:** `8888`

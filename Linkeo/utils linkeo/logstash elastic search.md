## description ( dans le site )
Logstash is an open source data collection engine with real-time pipelining capabilities. Logstash can dynamically unify data from disparate sources and normalize the data into destinations of your choice. Cleanse and democratize all your data for diverse advanced downstream analytics and visualization use cases.


```note
Un pipeline, dans le contexte de l'informatique et de la programmation, est une séquence d'opérations ou de traitements qui sont exécutés de manière séquentielle pour accomplir une tâche ou un processus complexe. Chaque étape du pipeline traite les données d'entrée et produit des résultats intermédiaires qui sont ensuite transmis à l'étape suivante pour traitement.
```

While Logstash originally drove innovation in log collection, its capabilities extend well beyond that use case. Any type of event can be enriched and transformed with a broad array of input, filter, and output plugins, with many native codecs further simplifying the ingestion process. Logstash accelerates your insights by harnessing a greater volume and variety of data.

## installation 

installtion de java-17 utilisant gestionnnaire de package system 
installation de logstash utilisant gestionnaire de paquet linux

## Utilisation 

- run the service by the following command  : 
```shell 
sudo systemctl start logstash.service
```

- allez dans le dossier d'installation 
```path 
usr/share/logstash
```
- exécution dans cette commande dans le dossier  : 
https://www.elastic.co/guide/en/logstash/8.8/first-event.html
```url 
cd logstash-8.8.2
bin/logstash  --path.settings -e 'input { stdin { } } output { stdout {} }'
```
<span class="remarque" >Remarque</span> rencontre d'une erreur sur  : 

```shell
Using bundled JDK: /usr/share/logstash/jdk
WARNING: Could not find logstash.yml which is typically located in $LS_HOME/config or /etc/logstash. You can specify the path using --path.settings. Continuing using the defaults
Could not find log4j2 configuration at path /usr/share/logstash/config/log4j2.properties. Using default config which logs errors to the console
[INFO ] 2023-07-18 09:26:59.461 [main] runner - Starting Logstash {"logstash.version"=>"8.8.2", "jruby.version"=>"jruby 9.3.10.0 (2.6.8) 2023-02-01 107b2e6697 OpenJDK 64-Bit Server VM 17.0.7+7 on 17.0.7+7 +indy +jit [x86_64-linux]"}
[INFO ] 2023-07-18 09:26:59.471 [main] runner - JVM bootstrap flags: [-Xms1g, -Xmx1g, -Djava.awt.headless=true, -Dfile.encoding=UTF-8, -Djruby.compile.invokedynamic=true, -XX:+HeapDumpOnOutOfMemoryError, -Djava.security.egd=file:/dev/urandom, -Dlog4j2.isThreadContextMapInheritable=true, -Djruby.regexp.interruptible=true, -Djdk.io.File.enableADS=true, --add-exports=jdk.compiler/com.sun.tools.javac.api=ALL-UNNAMED, --add-exports=jdk.compiler/com.sun.tools.javac.file=ALL-UNNAMED, --add-exports=jdk.compiler/com.sun.tools.javac.parser=ALL-UNNAMED, --add-exports=jdk.compiler/com.sun.tools.javac.tree=ALL-UNNAMED, --add-exports=jdk.compiler/com.sun.tools.javac.util=ALL-UNNAMED, --add-opens=java.base/java.security=ALL-UNNAMED, --add-opens=java.base/java.io=ALL-UNNAMED, --add-opens=java.base/java.nio.channels=ALL-UNNAMED, --add-opens=java.base/sun.nio.ch=ALL-UNNAMED, --add-opens=java.management/sun.management=ALL-UNNAMED]
Your settings are invalid. Reason: Path "/usr/share/logstash/data" must be a writable directory. It is not writable.
[FATAL] 2023-07-18 09:26:59.486 [main] Logstash - Logstash stopped processing because of an error: (SystemExit) exit
org.jruby.exceptions.SystemExit: (SystemExit) exit
	at org.jruby.RubyKernel.exit(org/jruby/RubyKernel.java:790) ~[jruby.jar:?]
	at org.jruby.RubyKernel.exit(org/jruby/RubyKernel.java:753) ~[jruby.jar:?]
	at usr.share.logstash.lib.bootstrap.environment.<main>(/usr/share/logstash/lib/bootstrap/environment.rb:91) ~[?:?]
```

## commande utilisé pour faire marchér code dans documentation 

https://www.elastic.co/guide/en/logstash/current/first-event.html

```shell 
sudo bin/logstash  --path.settings /home/rrakotoarinelina/Téléchargements/logstash-8.8.2/config/  -e 'input { stdin { } } output { stdout {} }'
```

N.B : le paramètre "--parth.settings chemin" doit être spécifié sinon on aura des erreurs.
## comment proceder à des vrais fichiers logs 

### il faut installer FileBeat

Before you create the Logstash pipeline, you’ll configure Filebeat to send log lines to Logstash. The [Filebeat](https://github.com/elastic/beats/tree/main/filebeat) client is a lightweight, resource-friendly tool that collects logs from files on the server and forwards these logs to your Logstash instance for processing.

https://www.elastic.co/guide/en/beats/filebeat/8.8/setup-repositories.html#_apt

installation filebeat avec apt 

- Download and install the Public Signing Key:
    
    wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
    
- You may need to install the `apt-transport-https` package on Debian before proceeding:
    
    sudo apt-get install apt-transport-https
    
- Save the repository definition to `/etc/apt/sources.list.d/elastic-8.x.list`:
    
    echo "deb https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-8.x.list
    
- Run `apt-get update`, and the repository is ready for use. For example, you can install Filebeat by running:
    
    sudo apt-get update && sudo apt-get install filebeat

N.B : s'il ya erreur il faut exucuter ces ommandes : 

```error 
Des valeurs entrant en conflit ont été renseignées pour l'option Signed-By à propos de la source https://artifacts.elastic.co/packages/8.x/apt/ stable: /usr/share/keyrings/elastic-keyring.gpg !=
```


```bash
sudo rm /etc/apt/sources.list.d/elastic-8.x.list
sudo rm /usr/share/keyrings/elastic-keyring.gpg
```

## tuto comprehension fonctionnement logstash 


![[logstash.png]]


logstash est un pipeline entrée - filtre  - sortie 
entrée est géré par filebeat, 

## filebeat (input)

### c'est quoi ?
Filebeat est un data shipper open-source développé par Elastic. Il fait partie de l'Elastic Stack (anciennement ELK Stack), qui comprend également Elasticsearch, Logstash et Kibana. Filebeat est spécifiquement conçu pour collecter, surveiller et expédier des fichiers de journaux (logs) à partir de différentes sources vers Elasticsearch ou Logstash pour un traitement ultérieur et une analyse.

### installation 
```shell
https://www.elastic.co/guide/en/beats/filebeat/current/setup-repositories.html
```
### dossier d'installation
le dossier filebeat installation se trouve dans /etc/filebeat

### service filebeat
Remarque : ne pas oublier der demarrer service filebeat aprés installtion , cela permet de configurer filebeat a demarraer au boot 

```shell
sudo systemctl enable filebeat
```

il faut démarrer le service de filebeat par cette commande  : 
```shell
sudo systemctl start filebeat
```

checker si status service filebeat
```shell
sudo service filebeat status
```

###  fichier de configuration filebeat 

on install filebeat et on config avec essentiellement dans un fichier filebeat.yml
filebeat peut avoir plusieurs intances qui peuvent collecter des données différentes ,
Il est recommandé de spécifié des paramètres unique pour chaque instance. 

Par exemple j'ai rencontré une erreur sur path.data locked en suivant le tuto, et la solution c'est de crée un yml unique pour chaque instance et y specifier un path.data et autre si nécessaire  :  
https://www.elastic.co/guide/en/beats/filebeat/master/configuration-path.html#_data, https://www.elastic.co/guide/en/beats/filebeat/master/directory-layout.html 
par exemple 
 - filebeat_instances1.yml

```yml
filebeat.inputs:
- type: log
  paths:
    - /var/logsForFilebeat/logstash-tutorial.log 
output.logstash:
  hosts: ["localhost:5044"]

path.data : /var/lib/filebeat_instance1

```

- input est de type log et se trouve dans le dossier renseigner dans paths, 
* path.data c'est le dossier dans lequelle filebeat va écrire ses data
- le port que logstash va ecouter c'est le 5044 

### option  "hosts"  : 

En termes simples, la ligne de configuration "hosts: ["localhost:5044"]" dans Filebeat indique à Filebeat où envoyer les données collectées à partir des fichiers de journaux.

Plus précisément, la configuration "hosts" spécifie l'adresse et le port du serveur de destination où Filebeat doit envoyer les données. Dans cet exemple, la valeur "localhost:5044" signifie que les données collectées par Filebeat seront envoyées à un serveur qui s'exécute localement (sur la même machine que Filebeat) et utilise le port 5044 pour écouter les données entrantes

### option "path.data"

En termes simples, "path.data" indique à Filebeat où stocker les informations qu'il utilise pour garder une trace des fichiers de journaux qu'il a déjà lus et expédiés. Cela permet à Filebeat de savoir quelles lignes de quel fichier il a déjà traitées, afin qu'il ne traite pas les mêmes données plusieurs fois.
## logstash

dossier d'installation  : /user/share/logstash 
il faut créer un fichier de configuration pour notre pipeline 

```shell
input {
    beats {
        port => "5044"
    }
}
# The filter part of this file is commented out to indicate that it is
# optional.
# filter {
#
# }
output {
    stdout { codec => rubydebug }
}
```

l'entrée est géré par filebeat
la sortie sera sur le console d'après ses instruction , on peut aussi avoir différent sorte de sortie comme dans un fichier par exemple 
## filtre grok 

### c'est quoi 

Grok est un outil puissant utilisé pour l'analyse et l'interprétation de données non structurées, souvent sous forme de lignes de texte, en extrayant des informations significatives et en les structurant en champs spécifiques. Grok est particulièrement utilisé dans le contexte de traitement de logs et de données de journalisation, où les informations peuvent être mélangées dans un texte non structuré.
### caractéristiques de Grok

1. **Modèles prédéfinis**:

Grok propose une bibliothèque de modèles prédéfinis pour des types de données couramment rencontrés, tels que les adresses IP, les dates, les URL, etc. Ces modèles aident à identifier et à extraire des informations spécifiques des données.
    
2. **Expressions régulières**:

Grok utilise des expressions régulières pour définir les motifs de texte que vous recherchez dans les données non structurées. Ces motifs sont associés aux modèles prédéfinis pour extraire des parties spécifiques du texte.
    
3. **Extraction de champs**: 

Grok permet d'extraire des morceaux de texte correspondant à des motifs spécifiques et de les organiser en champs structurés. Par exemple, à partir d'une ligne de journal contenant une adresse IP, une date et un message, Grok peut extraire chaque composant et les stocker dans des champs séparés.
    
4. **Personnalisation**: 

En plus des modèles prédéfinis, Grok permet de définir des modèles personnalisés pour répondre à des besoins spécifiques. Cela vous permet de créer des modèles adaptés à votre format de données.
    

Grok est largement utilisé dans les systèmes de gestion de logs et d'analyse de données, tels que Logstash (comme filtre de traitement de données) et d'autres outils similaires, pour normaliser les données non structurées et les rendre exploitables pour l'indexation, la recherche et l'analyse ultérieure. Il peut grandement simplifier le processus de traitement de données de logs en automatisant l'extraction d'informations pertinentes à partir de lignes de texte brutes.
### how to apply filter 

To apply a filter for a specific pattern of lines in a log file using tools like Logstash and Grok, follow these general steps:

1. **Identify the Pattern**: First, analyze the log file and identify the specific pattern you want to extract. This could be timestamps, IP addresses, error messages, or any other information that repeats in a predictable manner.
    
2. **Create a Grok Pattern**: Create a Grok pattern that matches the identified pattern in the log lines. Grok patterns are combinations of regular expressions and predefined patterns. If the predefined patterns don't cover your specific case, you can create custom patterns. A Grok pattern consists of `%{PATTERN_NAME:field}` where `PATTERN_NAME` is a predefined or custom pattern, and `field` is the name of the extracted field.
    
3. **Configure Logstash**: In your Logstash configuration file, define a filter section to apply the Grok pattern. This might look something like:
    
    plaintext

1. `filter {   grok {     match => { "message" => "%{TIMESTAMP_ISO8601:timestamp} %{IP:client_ip} %{GREEDYDATA:message}" }   } }`
    
    In this example, `%{TIMESTAMP_ISO8601}`, `%{IP}`, and `%{GREEDYDATA}` are predefined Grok patterns, and `timestamp`, `client_ip`, and `message` are field names where the extracted data will be stored.
    
2. **Apply the Filter**: The above configuration will apply the Grok filter to the `message` field of each log line. Adjust the field and pattern as needed based on your log file structure.
    
3. **Run Logstash**: Start Logstash with your configuration file. Logstash will process the log lines, apply the Grok filter, and create structured fields based on your pattern.
    
4. **Check the Output**: Verify that the filter is working as expected by checking the output. You can send the structured data to Elasticsearch or another destination for storage and analysis.
    
Keep in mind that log formats can vary, and creating an effective Grok pattern might require some trial and error. You can test your Grok patterns using online Grok pattern testers or tools within the Elastic Stack, which can help you fine-tune your patterns.

Remember that while Grok is powerful, it might not be suitable for every log parsing scenario. In some cases, other parsers or tools might be more appropriate, depending on the complexity of the log lines and the desired outcomes.

## Commandes pour utilisation logstash

il faut d'abord s'assurer que  : 

you don’t have to restart Logstash to pick up your changes. However, you do need to force Filebeat to read the log file from scratch. To do this, go to the terminal window where Filebeat is running and press Ctrl+C to shut down Filebeat. Then delete the Filebeat registry file. For example, run:

(dans le yml de filebeat  come path.data : /var/lib/filebeat_instance1/)

```shell
sudo rm -r /var/lib/filebeat_error/registry
```


```shell 
sudo rm -r /var/lib/filebeat_exception/registry
```


Since Filebeat stores the state of each file it harvests in the registry, deleting the registry file forces Filebeat to read all the files it’s harvesting from scratch.

Next, restart Filebeat with the following command:

```shell
sudo filebeat -e -c filebeat_instance_error.yml -d "publish" --path.data /var/lib/filebeat_error/
```


```shell
sudo filebeat -e -c filebeat_instance_exception.yml -d "publish" --path.data /var/lib/filebeat_exception/
```

REMARQUE : on a déjà specifié ce path.data dans le yml mais si cela n'est pas prise en compte (error sur locked data path), spécifier directement dans la commande à executer.

voici la commande pour vérifier la configuration de notre pipeline, si la config est bonne, on n'a pas d'erreur de sortie.
```shell
bin/logstash -f first-pipeline.conf --config.test_and_exit
```

Voici la commande pour demarrer logstash 

```shell
sudo bin/logstash -f zend2_pipeline_exception.conf --config.reload.automatic
```


```shell
sudo bin/logstash -f zend2_pipeline_error.conf --config.reload.automatic
```


The `--config.reload.automatic` option enables automatic config reloading so that you don’t have to stop and restart Logstash every time you modify the configuration file.

REMARQUE, si on a besoin de modifier des choses comme filebeat ou pipeline config, il faut juste refaire ces choses : 

- il n'est pas nécessaire de relancer logstash
- effacer filebeat registry 
- relancer filebeat 

doc https://www.elastic.co/guide/en/logstash/current/advanced-pipeline.html

## code php pour traiter json de sortie logstash

```php
// Open the JSON file for reading
$file = fopen('logs/ideo3.json', 'r');

$category = array();
// Process each line (entry) in the JSON file
while (($line = fgets($file)) !== false) {
    // Decode the JSON data for the current line
    $entry = json_decode($line, true);

    /*var_dump($entry);
    die();*/
    
    // Check if decoding was successful
    if ($entry !== null) {
        // Process the data for the current entry
        $timestamp = $entry["@timestamp"];
        $error_file = $entry["error_file"];
        $description =  isset($entry["description"])  ? $entry["description"] : $entry["message"];

        if (!in_array($description, $category)) {
            array_push($category, $description);
        }
        // Perform any other processing or output as needed
       /* echo "Timestamp: " . $timestamp . "<br>";
        echo "Log description: " . $description . "<br>";
        echo "error_file: " . $error_file . "<br>";
        echo "<hr>";*/
    } else {
        // Handle JSON parsing error for the current line if needed
        echo "Error parsing JSON data for line: " . $line . "<br>";
    }
}

// Close the file handle
fclose($file);

var_dump($category);

```



exepmple output console  : 

```shell 
{
        "loglevel" => "NOTICE",
     "description" => "A session had already been started - ignoring session_start()",
       "timestamp" => "2021-10-01T15:24:51+02:00",
           "event" => {
        "original" => "2021-10-01T15:24:51+02:00 NOTICE (5) A session had already been started - ignoring session_start() (errno 8) in /home/dev_jimmy/Projets_Linkeo/svn_icom3/icom3/branches/dev4769/#librairies/extension/ideo3/module/Application/src/Application/Controller/IndexController.php on line 36"
    },
         "message" => "2021-10-01T15:24:51+02:00 NOTICE (5) A session had already been started - ignoring session_start() (errno 8) in /home/dev_jimmy/Projets_Linkeo/svn_icom3/icom3/branches/dev4769/#librairies/extension/ideo3/module/Application/src/Application/Controller/IndexController.php on line 36",
            "tags" => [
        [0] "beats_input_codec_plain_applied"
    ],
             "log" => {
        "offset" => 308638,
          "file" => {
            "path" => "/var/www/html/testCode/logs/zend2/error/error20211001.log"
        }
    },
      "@timestamp" => 2023-08-08T08:46:49.725Z,
           "input" => {
        "type" => "log"
    },
           "agent" => {
                "name" => "TNV-DEV-0012",
                "type" => "filebeat",
             "version" => "8.9.0",
        "ephemeral_id" => "d84aa04b-cc7e-418b-bda2-aa43598f934f",
                  "id" => "f92594c6-862d-488d-9435-88a501fe9d71"
    },
        "@version" => "1",
     "line_number" => "36",
            "file" => "/home/dev_jimmy/Projets_Linkeo/svn_icom3/icom3/branches/dev4769/#librairies/extension/ideo3/module/Application/src/Application/Controller/IndexController.php",
             "ecs" => {
        "version" => "8.0.0"
    },
            "host" => {
        "name" => "TNV-DEV-0012"
    },
           "errno" => "8",
    "loglevel_num" => "5"
}

```
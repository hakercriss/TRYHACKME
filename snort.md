# La primera interacción con Snort
Primero, verifiquemos que snort está instalado. El siguiente comando le mostrará la versión de la instancia.
```bash
user@ubuntu$ snort -V

   ,,_     -*> Snort! <*-
  o"  )~   Version 2.9.7.0 GRE (Build XXXXXX) 
   ''''    By Martin Roesch & The Snort Team: http://www.snort.org/contact#team
           Copyright (C) 2014 Cisco and/or its affiliates. All rights reserved.
           Copyright (C) 1998-2013 Sourcefire, Inc., et al.
           Using libpcap version 1.9.1 (with TPACKET_V3)
           Using PCRE version: 8.39 2016-06-14
           Using ZLIB version: 1.2.11
```

#### Antes de ensuciarnos las manos, deberíamos asegurarnos de que nuestro archivo de configuración es válido.
Aquí se utiliza **"-T “** para probar la configuración, y **”-c”** para identificar el archivo de configuración (**snort.conf**).
Tenga en cuenta que es posible utilizar un archivo de configuración adicional señalándolo con **«-c»**. 
```bash
user@ubuntu$ sudo snort -c /etc/snort/snort.conf -T 

        --== Initializing Snort ==--
Initializing Output Plugins!
Initializing Preprocessors!
Initializing Plug-ins!
... [Output truncated]
        --== Initialization Complete ==--

   ,,_     -*> Snort! <*-
  o"  )~   Version 2.9.7.0 GRE (Build XXXX) 
   ''''    By Martin Roesch & The Snort Team: http://www.snort.org/contact#team
           Copyright (C) 2014 Cisco and/or its affiliates. All rights reserved.
           Copyright (C) 1998-2013 Sourcefire, Inc., et al.
           Using libpcap version 1.9.1 (with TPACKET_V3)
           Using PCRE version: 8.39 2016-06-14
           Using ZLIB version: 1.2.11

           Rules Engine: SF_SNORT_DETECTION_ENGINE  Version 2.4  
           Preprocessor Object: SF_GTP  Version 1.1  
           Preprocessor Object: SF_SIP  Version 1.1  
           Preprocessor Object: SF_SSH  Version 1.1  
           Preprocessor Object: SF_SMTP  Version 1.1  
           Preprocessor Object: SF_POP  Version 1.0  
           Preprocessor Object: SF_DCERPC2  Version 1.0  
           Preprocessor Object: SF_IMAP  Version 1.0  
           Preprocessor Object: SF_DNP3  Version 1.1  
           Preprocessor Object: SF_SSLPP  Version 1.1  
           Preprocessor Object: SF_MODBUS  Version 1.1  
           Preprocessor Object: SF_SDF  Version 1.1  
           Preprocessor Object: SF_REPUTATION  Version 1.1  
           Preprocessor Object: SF_DNS  Version 1.1  
           Preprocessor Object: SF_FTPTELNET  Version 1.2  
... [Output truncated]
Snort successfully validated the configuration!
Snort exiting
```
Una vez que usamos un archivo de configuración, ¡snort tiene mucho más poder! El fichero de configuración es un fichero de gestión todo-en-uno del snort. Aquí se identifican las reglas, plugins, mecanismos de detección, acciones por defecto y ajustes de salida. Es posible tener múltiples archivos de configuración para diferentes propósitos y casos, pero sólo se puede utilizar uno en tiempo de ejecución.

Tenga en cuenta que cada vez que inicie el Snort, éste mostrará automáticamente el banner por defecto y la información inicial sobre su configuración. Puede evitarlo utilizando el parámetro «-q» .

| **Parámetro** | **Descripción**                                                                 |
|---------------|---------------------------------------------------------------------------------|
| **-V / --version**| Este parámetro proporciona información sobre la versión de su instancia.   |
| **-c**         | Identificación del archivo de configuración.                                   |
| **-T**         | Parámetro de autocomprobación de Snort, puede probar su configuración con este parámetro. |
| **-q**         | Modo silencioso, evita que Snort muestre el banner por defecto y la información inicial sobre su configuración. |


Eso fue fácil; ¡continuemos explorando los modos de snort!

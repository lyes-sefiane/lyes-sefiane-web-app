## Lyes Sefiane | Software Engineer 3 𓂀 | Professional Profile

* TODO

## Deploy with NGINX and Docker

### Build Docker Image

```bash
Lyes Sefiane@DESKTOP-EJF2R0S MINGW64 ~/Documents/eclipse-workspace/lyes-sefiane (main)
$ docker build -t lyes-sefiane-professional-profile:latest .
[+] Building 14.5s (7/7) FINISHED                                                                                                  docker:default
 => [internal] load build definition from Dockerfile                                                                                         0.1s
 => => transferring dockerfile: 104B                                                                                                         0.0s
 => [internal] load .dockerignore                                                                                                            0.1s
 => => transferring context: 383B                                                                                                            0.0s
 => [internal] load metadata for docker.io/library/nginx:1.25.4-alpine                                                                       2.9s
 => [internal] load build context                                                                                                            0.4s
 => => transferring context: 10.12MB                                                                                                         0.3s
 => [1/2] FROM docker.io/library/nginx:1.25.4-alpine@sha256:6a2f8b28e45c4adea04ec207a251fd4a2df03ddc930f782af51e315ebc76e9a9                 9.5s
 => => resolve docker.io/library/nginx:1.25.4-alpine@sha256:6a2f8b28e45c4adea04ec207a251fd4a2df03ddc930f782af51e315ebc76e9a9                 0.1s 
 => => sha256:6a2f8b28e45c4adea04ec207a251fd4a2df03ddc930f782af51e315ebc76e9a9 8.71kB / 8.71kB                                               0.0s
 => => sha256:6913ed9ec8d009744018c1740879327fe2e085935b2cce7a234bf05347b670d7 11.74kB / 11.74kB                                             0.0s
 => => sha256:cb0953165f59b5cf2227ae979a49a2284956d997fad4ed7a338eebc6aef3e70b 2.50kB / 2.50kB                                               0.0s 
 => => sha256:619be1103602d98e1963557998c954c892b3872986c27365e9f651f5bc27cab8 3.40MB / 3.40MB                                               2.3s 
 => => sha256:018b9065ed0dfedff48bbd11f6014960bb496e71c395f772bfad123ab33a1800 1.90MB / 1.90MB                                               2.3s 
 => => sha256:c3ea3344e711fd7111dee02f17deebceb725ed1d0ee998f7fb472114dc1399ce 629B / 629B                                                   2.2s 
 => => sha256:c7059f3102784cd05dc96fff74a52bce9fa50fea724ece08748507fa3455999b 956B / 956B                                                   2.6s 
 => => extracting sha256:619be1103602d98e1963557998c954c892b3872986c27365e9f651f5bc27cab8                                                    0.2s
 => => sha256:a101c9a82b88a3fa561030af162d98a130ca3bc0501b2e70594410dd426f2c9b 393B / 393B                                                   2.7s 
 => => sha256:d6a456492aaa4c003389fec3da0939f31c505232fcf1925db314815a196c444f 1.21kB / 1.21kB                                               2.7s 
 => => extracting sha256:018b9065ed0dfedff48bbd11f6014960bb496e71c395f772bfad123ab33a1800                                                    0.5s 
 => => sha256:e1c681003a03fff277ecf90fccf526881bcc2e006c9e371b58f45680d54c1954 1.40kB / 1.40kB                                               2.9s 
 => => sha256:a85ccd8c07bd7090e8a37ab878413b035a370e872367b145a0c0aaaaf60ccbdf 12.65MB / 12.65MB                                             8.3s 
 => => extracting sha256:c3ea3344e711fd7111dee02f17deebceb725ed1d0ee998f7fb472114dc1399ce                                                    0.0s 
 => => extracting sha256:c7059f3102784cd05dc96fff74a52bce9fa50fea724ece08748507fa3455999b                                                    0.0s 
 => => extracting sha256:a101c9a82b88a3fa561030af162d98a130ca3bc0501b2e70594410dd426f2c9b                                                    0.0s 
 => => extracting sha256:d6a456492aaa4c003389fec3da0939f31c505232fcf1925db314815a196c444f                                                    0.0s 
 => => extracting sha256:e1c681003a03fff277ecf90fccf526881bcc2e006c9e371b58f45680d54c1954                                                    0.0s
 => => extracting sha256:a85ccd8c07bd7090e8a37ab878413b035a370e872367b145a0c0aaaaf60ccbdf                                                    0.8s 
 => [2/2] COPY . /usr/share/nginx/html                                                                                                       1.5s 
 => exporting to image                                                                                                                       0.1s 
 => => exporting layers                                                                                                                      0.1s 
 => => writing image sha256:195f3f7418d59f3db3d33bd10eb5b861b5ad2658920ade675b1ccf76259ba206                                                 0.0s 
 => => naming to docker.io/library/lyes-sefiane-professional-profile:latest                                                                  0.0s 

What's Next?
  View a summary of image vulnerabilities and recommendations → docker scout quickview
```

### Deploy

```bash
Lyes Sefiane@DESKTOP-EJF2R0S MINGW64 ~/Documents/eclipse-workspace/lyes-sefiane (main)
$ chmod +x deploy 

Lyes Sefiane@DESKTOP-EJF2R0S MINGW64 ~/Documents/eclipse-workspace/lyes-sefiane (main)
$ ./deploy

 ######
 #     # ###### #####  #       ####  #   # #    # ###### #    # #####
 #     # #      #    # #      #    #  # #  ##  ## #      ##   #   #
 #     # #####  #    # #      #    #   #   # ## # #####  # #  #   #
 #     # #      #####  #      #    #   #   #    # #      #  # #   #
 #     # #      #      #      #    #   #   #    # #      #   ##   #
 ######  ###### #      ######  ####    #   #    # ###### #    #   #

 #     #  #####  ### #     # #     #             ######
 ##    # #     #  #  ##    #  #   #       #      #     #  ####   ####  #    # ###### #####
 # #   # #        #  # #   #   # #        #      #     # #    # #    # #   #  #      #    #
 #  #  # #  ####  #  #  #  #    #       #####    #     # #    # #      ####   #####  #    #
 #   # # #     #  #  #   # #   # #        #      #     # #    # #      #  #   #      #####
 #    ## #     #  #  #    ##  #   #       #      #     # #    # #    # #   #  #      #   #
 #     #  #####  ### #     # #     #             ######   ####   ####  #    # ###### #    #

MINGW64_NT-10.0-19045 : Hi 😊 ! please make a selection.

1) Docker Run
2) Docker Stop
3) Docker Remove
4) quit
#? 1
Start Container: lyes-sefiane-professional-profile ...
e38b1fde5b2acba2dbdf29e27d7a09c92d27d2d27b8f261323d663c5dca409ea
```

### URL

* http://localhost:8080/


## Deploy to Firebase

* TODO

## Contributing

Pull requests are welcome. 

For major changes, please open an issue first to discuss what you would like to change.


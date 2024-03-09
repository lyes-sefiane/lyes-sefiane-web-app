## License

[Creative Commons Attribution-NonCommercial-NoDerivs 4.0 International License][cc-by-nc-nd].

[![CC BY-NC-ND 4.0][cc-by-nc-nd-image]][cc-by-nc-nd]

[cc-by-nc-nd]: http://creativecommons.org/licenses/by-nc-nd/4.0/
[cc-by-nc-nd-image]: https://licensebuttons.net/l/by-nc-nd/4.0/88x31.png
[cc-by-nc-nd-shield]: https://img.shields.io/badge/License-CC%20BY--NC--ND%204.0-lightgrey.svg

## Lyes Sefiane | Software Engineer 3 𓂀 | Professional Profile

<p align="center">
    <img src="https://raw.githubusercontent.com/lyes-s/lyes-sefiane/main/images/lyes-sefiane-web-app.PNG">
</p>

* Website URL: https://lyes-sefiane.web.app

## Table Of Contents

  * [Build and Publish Docker Image to DockerHub with GitHub Actions](#build-and-publish-docker-image-to-dockerhub-with-github-actions)
      * [GitHub Actions: Docker Job Description](#github-action-docker-job-description)

  * [GitHub Integration with Dockerhub](#github-integration-with-dockerhub)

  * [Deploy Static Website to Firebase Hosting with GitHub Actions](#deploy-static-website-to-firebase-hosting-with-github-actions)
      * [GitHub Actions Generated by the Firebase CLI](#github-actions-generated-by-the-firebase-cli)
      * [GitHub Actions: Firebase Deploy Job Description](#github-actions-generated-by-the-firebase-cli)
  
  * [GitHub Integration with Firebase](#github-integration-with-firebase)

  * [Localhost : Deploy with NGINX and Docker](#localhost-deploy-with-nginx-and-docker)
      * [Build Docker Image](#build-docker-image)
      * [NGINX and Docker](#nginx-and-docker)
      * [URL](#url)

  * [Deploy Static Website to Firebase Hosting with Firebase CLI](#deploy-static-website-to-firebase-hosting-with-firebase-cli)
      * [Firebase CLI: Initialization and Deploy](#firebase-cli-initialization-and-deploy)
      * [Firebase CLI: Login & Deploy](#firebase-cli-login--deploy)


## Build and Publish Docker Image to DockerHub with GitHub Actions

### GitHub Action Docker Job Description

```bash
  # Build Docker Image and Publish it to Dockerhub.
  dockerhub_deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Set up QEMU
        uses: docker/setup-qemu-action@v3
      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3
      - name: Login to Docker Hub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}
      - name: set env
        run: | 
            echo "RELEASE_VERSION=${GITHUB_REF#refs/*/}" >> $GITHUB_ENV  
            echo "DATE_NOW=$(date +'%Y-%m-%d_%H-%M-%S_')" >> $GITHUB_ENV
      - name: Build and push
        uses: docker/build-push-action@v5
        with:
          push: true
          tags: |
            ${{ secrets.DOCKERHUB_USERNAME }}/${{ secrets.DOCKERHUB_REPOSITORY }}:${{ secrets.DOCKER_IMAGE_TAG_LATEST }}
            ${{ secrets.DOCKERHUB_USERNAME }}/${{ secrets.DOCKERHUB_REPOSITORY }}:${{ env.DATE_NOW }}${{env.RELEASE_VERSION}}
```
## GitHub Integration with Dockerhub

<p align="center">
    <img src="https://raw.githubusercontent.com/lyes-s/lyes-sefiane/main/images/docker-image-build.PNG">
</p>

<p align="center">
    <img src="https://raw.githubusercontent.com/lyes-s/lyes-sefiane/main/images/docker-image-publish-to-dockerhub.PNG">
</p>

## Deploy Static Website to Firebase Hosting with GitHub Actions

### GitHub Actions Generated by the Firebase CLI

```bash
Lyes Sefiane@DESKTOP-EJF2R0S MINGW64 ~
$ firebase login --interactive
i  Firebase optionally collects CLI and Emulator Suite usage and error reporting information to help improve our products. Data is collected in accordance with Google's privacy policy (https://policies.google.com/privacy) and is not used to identify you.

? Allow Firebase to collect CLI and Emulator Suite usage and error reporting                 n
? Allow Firebase to collect CLI and Emulator Suite usage and error reporting
information? No

Visit this URL on this device to log in:
https://accounts.google.com/o/oauth2/auth?client_id=563584335869-fgrhgmd47bqnekij5i8b5pr03ho849e6.apps.googleusercontent.com&scope=email%20openid%20https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcloudplatformprojects.readonly%20https%3A%2F%2Fwww.googleapis.com%2Fauth%2Ffirebase%20https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcloud-platform&response_type=code&state=625452047&redirect_uri=http%3A%2F%2Flocalhost%3A9005

Waiting for authentication...

+  Success! Logged in as lyes.sefiane@gmail.com

Lyes Sefiane@DESKTOP-EJF2R0S MINGW64 ~
$ cd Documents/eclipse-workspace/lyes-sefiane

Lyes Sefiane@DESKTOP-EJF2R0S MINGW64 ~/Documents/eclipse-workspace/lyes-sefiane (main)
$ firebase init hosting:github

     ######## #### ########  ######## ########     ###     ######  ########
     ##        ##  ##     ## ##       ##     ##  ##   ##  ##       ##
     ######    ##  ########  ######   ########  #########  ######  ######
     ##        ##  ##    ##  ##       ##     ## ##     ##       ## ##
     ##       #### ##     ## ######## ########  ##     ##  ######  ########

You're about to initialize a Firebase project in this directory:

  C:\Users\Lyes Sefiane\Documents\eclipse-workspace\lyes-sefiane

Before we get started, keep in mind:

  * You are initializing within an existing Firebase project directory

? Are you ready to proceed? (Y/n) y
? Are you ready to proceed? Yes

=== Project Setup

First, let's associate this project directory with a Firebase project.
You can create multiple project aliases by running firebase use --add,
but for now we'll just set up a default project.

i  Using project lyes-sefiane (lyes-sefiane)

=== Hosting:github Setup

i  Detected a .git folder at C:\Users\Lyes Sefiane\Documents\eclipse-workspace\lyes-sefiane
i  Authorizing with GitHub to upload your service account to a GitHub repository's secrets store.

Visit this URL on this device to log in:
https://github.com/login/oauth/authorize?client_id=89cf50f02ac6aaed3484&state=634400349&redirect_uri=http%3A%2F%2Flocalhost%3A9005&scope=read%3Auser%20repo%20public_repo

Waiting for authentication...

+  Success! Logged into GitHub as lyes-s

? For which GitHub repository would you like to set up a GitHub workflow?                    l
? For which GitHub repository would you like to set up a GitHub workflow?
- Retrieving a service account.s/lyes-sefiane

+  Created service account github-action-765964405 with Firebase Hosting admin permissions.
- Uploading service account secrets to repository: lyes-s/lyes-sefiane
+  Uploaded service account JSON to GitHub as secret FIREBASE_SERVICE_ACCOUNT_LYES_SEFIANE.
i  You can manage your secrets at https://github.com/lyes-s/lyes-sefiane/settings/secrets.

? Set up the workflow to run a build script before every deploy? (y/N) y
? Set up the workflow to run a build script before every deploy? Yes
? What script should be run before every deploy? (npm ci && npm run build)
? What script should be run before every deploy? npm ci && npm run build

+  Created workflow file C:\Users\Lyes Sefiane\Documents\eclipse-workspace\lyes-sefiane\.github/workflows/firebase-hosting-pull-request.yml
? Set up automatic deployment to your site's live channel when a PR is merged?
? What is the name of the GitHub branch associated with your site's live
channel? main
+  Created workflow file C:\Users\Lyes Sefiane\Documents\eclipse-workspace\lyes-sefiane\.github/workflows/firebase-hosting-merge.yml

i  Action required: Visit this URL to revoke authorization for the Firebase CLI GitHub OAuth App:
https://github.com/settings/connections/applications/89cf50f02ac6aaed3484
i  Action required: Push any new workflow file(s) to your repo

i  Writing configuration info to firebase.json...
i  Writing project information to .firebaserc...

+  Firebase initialization complete!

Lyes Sefiane@DESKTOP-EJF2R0S MINGW64 ~/Documents/eclipse-workspace/lyes-sefiane (main)
```
### GitHub Action Firebase Deploy Job Description

```bash
  # Deploy the static website to Firebase.
  firebase_deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
    # - run: npm ci && npm run build
      - uses: FirebaseExtended/action-hosting-deploy@v0
        with:
          repoToken: '${{ secrets.GITHUB_TOKEN }}'
          firebaseServiceAccount: '${{ secrets.FIREBASE_SERVICE_ACCOUNT_LYES_SEFIANE }}'
          channelId: live
          projectId: '${{ secrets.FIREBASE_PROJECT_ID_LYES_SEFIANE }}'
```

## GitHub Integration with Firebase

<p align="center">
    <img src="https://raw.githubusercontent.com/lyes-s/lyes-sefiane/main/images/firebase-deploy.PNG">
</p>

<p align="center">
    <img src="https://raw.githubusercontent.com/lyes-s/lyes-sefiane/main/images/firebase.PNG">
</p>

## Localhost Deploy with NGINX and Docker

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

### NGINX and Docker

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

## Deploy Static Website to Firebase Hosting with Firebase CLI

### Firebase CLI: Initialization and Deploy

```bash
C:\Users\Lyes Sefiane>firebase login
i  Firebase optionally collects CLI and Emulator Suite usage and error reporting information to help improve our products. Data is collected in accordance with Google's privacy policy (https://policies.google.com/privacy) and is not used to identify you.

? Allow Firebase to collect CLI and Emulator Suite usage and error reporting information? No

Visit this URL on this device to log in:
https://accounts.google.com/o/oauth2/auth?client_id=563584335869-fgrhgmd47bqnekij5i8b5pr03ho849e6.apps.googleusercontent.com&scope=email%20openid%20https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcloudplatformprojects.readonly%20https%3A%2F%2Fwww.googleapis.com%2Fauth%2Ffirebase%20https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcloud-platform&response_type=code&state=268374151&redirect_uri=http%3A%2F%2Flocalhost%3A9005

Waiting for authentication...

+  Success! Logged in as lyes.sefiane@gmail.com

C:\Users\Lyes Sefiane\Documents\eclipse-workspace\lyes-sefiane>firebase init

     ######## #### ########  ######## ########     ###     ######  ########
     ##        ##  ##     ## ##       ##     ##  ##   ##  ##       ##
     ######    ##  ########  ######   ########  #########  ######  ######
     ##        ##  ##    ##  ##       ##     ## ##     ##       ## ##
     ##       #### ##     ## ######## ########  ##     ##  ######  ########

You're about to initialize a Firebase project in this directory:

  C:\Users\Lyes Sefiane\Documents\eclipse-workspace\lyes-sefiane

? Are you ready to proceed? Yes
? Which Firebase features do you want to set up for this directory? Press Space to select features, then Enter to confirm your choices. Hosting: Configure files for
Firebase Hosting and (optionally) set up GitHub Action deploys

=== Project Setup

First, let's associate this project directory with a Firebase project.
You can create multiple project aliases by running firebase use --add,
but for now we'll just set up a default project.

? Please select an option: Use an existing project
? Select a default Firebase project for this directory: lyes-sefiane (lyes-sefiane)
i  Using project lyes-sefiane (lyes-sefiane)

=== Hosting Setup

Your public directory is the folder (relative to your project directory) that
will contain Hosting assets to be uploaded with firebase deploy. If you
have a build process for your assets, use your build's output directory.

? What do you want to use as your public directory? public
? Configure as a single-page app (rewrite all urls to /index.html)? No
? Set up automatic builds and deploys with GitHub? No
+  Wrote public/404.html
+  Wrote public/index.html

i  Writing configuration info to firebase.json...
i  Writing project information to .firebaserc...
i  Writing gitignore file to .gitignore...

+  Firebase initialization complete!

C:\Users\Lyes Sefiane\Documents\eclipse-workspace\lyes-sefiane>firebase deploy

=== Deploying to 'lyes-sefiane'...

i  deploying hosting
i  hosting[lyes-sefiane]: beginning deploy...

+  hosting[lyes-sefiane]: file upload complete
i  hosting[lyes-sefiane]: finalizing version...
+  hosting[lyes-sefiane]: version finalizedkspace\lyes-sefiane>firebase deploy
i  hosting[lyes-sefiane]: releasing new version...
+  hosting[lyes-sefiane]: release complete

+  Deploy complete!g
i  hosting[lyes-sefiane]: beginning deploy...
Project Console: https://console.firebase.google.com/project/lyes-sefiane/overview
Hosting URL: https://lyes-sefiane.web.app

C:\Users\Lyes Sefiane\Documents\eclipse-workspace\lyes-sefiane>
```

### Firebase CLI: Login & Deploy

```bash
Lyes Sefiane@DESKTOP-EJF2R0S MINGW64 ~/Documents/eclipse-workspace/lyes-sefiane (main)
$ firebase login --interactive
i  Firebase optionally collects CLI and Emulator Suite usage and error reporting information to help improve our products. Data is collected in accordance with Google's privacy policy (https://policies.google.com/privacy) and is not used to identify you.

? Allow Firebase to collect CLI and Emulator Suite usage and error reporting
information? No
Visit this URL on this device to log in:
https://accounts.google.com/o/oauth2/auth?client_id=563584335869-fgrhgmd47bqnekij5i8b5pr03ho849e6.apps.googleusercontent.com&scope=email%20openid%20https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcloudplatformprojects.readonly%20https%3A%2F%2Fwww.googleapis.com%2Fauth%2Ffirebase%20https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcloud-platform&response_type=code&state=699217391&redirect_uri=http%3A%2F%2Flocalhost%3A9005

Waiting for authentication...

+  Success! Logged in as lyes.sefiane@gmail.com

Lyes Sefiane@DESKTOP-EJF2R0S MINGW64 ~/Documents/eclipse-workspace/lyes-sefiane (main)
$ firebase deploy

=== Deploying to 'lyes-sefiane'...

i  deploying hosting
i  hosting[lyes-sefiane]: beginning deploy...
i  hosting[lyes-sefiane]: found 145 files in /
i  hosting: upload complete
+  hosting[lyes-sefiane]: file upload complete
i  hosting[lyes-sefiane]: finalizing version...
+  hosting[lyes-sefiane]: version finalized
i  hosting[lyes-sefiane]: releasing new version...
+  hosting[lyes-sefiane]: release complete

+  Deploy complete!

Project Console: https://console.firebase.google.com/project/lyes-sefiane/overview
Hosting URL: https://lyes-sefiane.web.app


Lyes Sefiane@DESKTOP-EJF2R0S MINGW64 ~/Documents/eclipse-workspace/lyes-sefiane (main)
$ firebase logout
+  Logged out from lyes.sefiane@gmail.com

```

## Contributing

Pull requests are welcome. 

For major changes, please open an issue first to discuss what you would like to change.


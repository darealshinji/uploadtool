# uploadtool
Upload builds to GitHub Releases easily

## Purpose
Super simple uploading of continuous builds (each push) to GitHub Releases.

## Usage

Upon each run, this script will _delete_ any pre-existing release and tag with the name `continuous`, create a new one, and upload the specified binaries there.

 - On https://github.com/settings/tokens, click on "Generate new token" and generate a token with at least the `public_repo`, `repo:status`, and `repo_deployment` scopes
 - On Travis CI, go to the settings of your project at `https://travis-ci.org/yourusername/yourrepository/settings`
 - Under "Environment Variables", add key `GITHUB_TOKEN` and the token you generated above as the value. Make sure that "Display value in build log" is set to "OFF"
 - In the `.travis.yml` of your GitHub repository, add something like this:
 
 ```
 after_success:
  - ls -lh out/* # Assuming you have some files in out/ that you would like to upload
  - wget -c https://github.com/probonopd/uploadtool/raw/master/upload.sh
  - bash ./upload.sh out/*
 ```

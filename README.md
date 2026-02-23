
## Static Site on GCS

#### Set Variables
```sh
export GCP_PROJECT_ID=""
export SITE="my-static-site-$(date +%s)"
```

#### Create Bucket
```sh
gsutil -u "$GCP_PROJECT_ID" mb -c "STANDARD" -l US "gs://$SITE" 
```
or
```sh
gcloud storage buckets create "gs://$SITE" --location "US" --project -u "$GCP_PROJECT_ID"
```

#### Add Files
Upload all files
```sh
gsutil -u "$GCP_PROJECT_ID" -m "cp" -r "index.html" "style.css" "script.js" "gs://$SITE/"
```

Or upload entire directory
```sh
gsutil -u "$GCP_PROJECT_ID" -m "cp" -r "./my-site/*" "gs://$SITE/"
```

#### Set Main Page and Error Page
```sh
gsutil -u "$GCP_PROJECT_ID" web set -m "index.html" -e "404.html" "gs://$SITE"
```

#### Access Your Site
```sh
open "https://storage.googleapis.com/$SITE/index.html"
```

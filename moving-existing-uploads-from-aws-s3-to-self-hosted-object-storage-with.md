# Moving existing uploads from AWS S3 to self-hosted object storage with rclone

Switching an app from AWS S3 to self-hosted S3-compatible storage is mostly a config change. The files are the slow part. rclone handles it well.

## Configure both remotes

```
rclone config create aws s3 provider AWS env_auth true region eu-central-1
rclone config create local s3 provider Minio endpoint https://s3.example.com access_key_id KEY secret_access_key SECRET
```

## Copy in passes

1. Initial bulk copy while the app still writes to AWS: `rclone copy aws:app-uploads local:app-uploads --transfers 16 --checksum`.
2. Repeat the same command. Only new and changed objects move.
3. Switch the app's endpoint and credentials to the new server and deploy.
4. Final `rclone copy` to catch objects written during the switch.
5. `rclone check aws:app-uploads local:app-uploads` to confirm counts and hashes.

## Watch for

- AWS egress charges on large buckets. Estimate before you start.
- Public URLs hard-coded in the database. Rewrite them or keep a redirect.
- Bucket policies and CORS rules, which rclone does not copy.

Keep the AWS bucket read-only for a few weeks before deleting it. Setup for [self-hosted MinIO object storage](https://peon.sh/blogs/self-host-minio-object-storage) is on the Peon blog. Notes by a contributor to [Peon](https://peon.sh/), an open-source self-hosted deployment platform.

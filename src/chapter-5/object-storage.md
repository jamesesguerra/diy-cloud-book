# Object Storage
The next thing our app needs is a way to store blobs, objects, and essentially, images. This will serve as our equivalent of Amazon S3 or Azure Blob Storage. There are several open-source and self-hostable options available, such as [Ceph](https://ceph.io/en/), [SeaweedFS](https://github.com/seaweedfs/seaweedfs), and [Garage](https://garagehq.deuxfleurs.fr/). I personally haven't tried them but have heard good things. The one that consistently comes up the most, and the one we’ll be using, is [MinIO](https://www.min.io/).

## Why MinIO?
I'm choosing MinIO because it's a lightweight yet high performance object storage solution that’s designed to be simple to deploy and easy to scale. It’s one of the most popular self-hosted alternatives to commercial cloud storage services like Amazon S3 or Azure Blob Storage.

One of its biggest strengths is that it’s fully S3 API compatible, meaning any application or SDK that works with Amazon S3 will also work seamlessly with it. This makes it incredibly easy to integrate into existing apps or migrate workloads without changing your code.

## Setting up MinIO
---
created: 1655018433097
desc: ''
id: faxbzx44mmk9u2ix1fdfuu7
title: S3
updated: 1655540930748
---
   
You can turn on versioning to use S3 as a repository.   
   
## [AWS CodePipeline](../devlog/AWS%20CodePipeline.md) Artifacts   
   
The artifact when S3 is the source is always the same object key. The new version of the object (same key) is what leads to the pipeline triggering.   
   
## ACL   
   
Setting ACL to private doesn’t really protect it, object may have public even though bucket might be private, so both bucket and object must be private.
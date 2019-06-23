**1.  What happens when I run `docker container run my-image`?**

a)	A copy of “my-image” is created to allow writing to it
	
*Explanation: One of the main benefits of using containers is the saving of disk space. Having copies of images is against this principle.*

b)	A new rewritable layer is created on top of `my-image` **(correct)**

*Explanation: A thin container layer is added on top of the image. This explains too why running containers is so fast.*
		
c)	An error occurs

*Explanation: An error might occur if `my-image` doesn’t exist locally, or it cannot be retrieved from the standard image registry, DockerHub. But if we assume that the image is available, no error should occur.*

**2.	 The process for building an image layer is listed below. Which one of these steps doesn't belong to this process?**
	
a)	Read a command from the Dockerfile
	
b)	Run an intermediate container on top of the previous image
	
c)	Execute the Dockerfile command
	
d)	Commit the intermediate container
	
e)	Remove the previous image **(correct)**

*Explanation: If the previous image is removed, the next intermediate container won’t be able to start, because image layers depend on each other. This is an advanced topic that we will see with “Layer Caching”.*

The following contents also exists as a Katacoda scenario. Check it on this link: [https://www.katacoda.com/houssein/scenarios/build-images](https://www.katacoda.com/houssein/scenarios/build-images).

# Building Images with Dockerfiles

In this exercise, you will:

 - Write your first Dockerfile using the `RUN` and `CMD` instructions
 - Build an image from the Dockerfile
 - See how layer caching reduces the build time

## Writing the Dockerfile

1. Create an empty directory `myDir`, and `cd` into it:

	```
	$ mkdir myDir; cd myDir
	```

2. Create a file `Dockerfile` (with `D` uppercase), and paste following content:

	```
	FROM ubuntu
	RUN apt-get update && apt-get install -y iputils-ping 
	CMD ping -c 5 8.8.8.8
	```
	
	> Question: Looking at this Dockerfile, what will be the base image of our final image?
	
	If you say it's `Ubuntu`, you got it right. And if you guessed the `latest` tag, you're even righter. You can see tags as versions. Since we didn't specify any tag after the image name, `latest` is picked. Don't worry if you never heard of *tags*, we will talk about this image property in a more advanced topic.

	The second line of the Dockerfile will execute an update of `apt-get`, the package manager, then install the ping tool.
	
	The final line of the Dockerfile sets a default command to the final image. This default command is not executed during the image build, but rather when a container is launched based on the final image. We'll see this in action in a minute.
	
## Building the image

1. While inside the `myDir` folder, run following command:

	```
	$ time docker image build -t mypinger .
	```
	
	`time`, at the beginning of the command, is not necessary for the build. It will just show us how much time did the build take.
	
	The `-t` flag is to set the name of the final image, here we'll call it `mypinger`.
		
	**Note the dot** `.` at the end of the command, this is to set the build context, where Docker looks for the Dockerfile. In this case it's the current directory.
	
	If everything goes fine, you should see `Successfully tagged mypinger:latest` at the end of the output, in addition to the time taken by the build process.
	
2. Now run the same build command again, and notice how fast is the build!

	Comapre the time of the first build attempt with the second one.
	
	> Question: What do you think has made the build much faster the second time?
	
	If you check the output of the build command, you'll see several times `---> Using cache`. Layers that have been built before, are just reused! We will talk about caching in more detail in a more advanced chapter.
	
## Running a container

Run a container based on your own image to see the output of the `ping` command that was defined in the `CMD` instruction:

	```
	$ docker container run mypinger
	```
	
## Conclusion

In this exercise, you built your own Dockerfile, where you used:

- the `FROM`instruction to define a base image
- the`RUN` instruction to update your environment and to install a required tool
- the `CMD` instruction to set the default command of your image.

You saw also briefly the effect of layer caching. In the next chapter we will see how to leverage layer caching and sharing. 
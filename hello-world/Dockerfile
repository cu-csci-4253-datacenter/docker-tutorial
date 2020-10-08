#
# Your dockerfile is typically based on an earlier image.
# The format is "name:tag" where tag names a specific version.
# The tag "latest" refers to, obviously, the latest version.
# Your should use an explicit version and not "latest" because
# the ability to rebuild your image depends on having a known base.
# The "latest" tag may change from one build to the next.
#
FROM ubuntu:20.04

#
# RUN commands modify the build image so far. Each RUN adds a "layer"
# to the stackable image; it's common to see compound shell commands
# separated by "&&" (only continue if command succeeds) and "\" (line continuation).
#
# Is using package managers, they will only have old (or missing) state and you'll
# need to update them to include current repositories. You'll need to provide options
# that 
#

RUN	DEBIAN_FRONTEND=noninteractive apt-get update -y && \
	apt-get install -yq --no-install-recommends \
	   nginx

#
# When you build an image, you specify the "context" or directory from which
# included files can be pulled. You can then COPY or ADD files to the build
# image from that context
#
COPY	index.html	/var/www/html

#
# Containers communicate with the outside world through network ports and storage through volumes.
#
EXPOSE	80

#
# We can also specify where we expect external volumes to be mounted
#
VOLUME	/var/www/html/dir

#
# Docker runs a single process from which all other processes
# are spawned. In UNIX systems, which would typically be an "init"
# process that then spawns applications using mechanisms like systemd
#
# In this example just start nginx directly; it spawns web servers and
# then exits. That means the container will just exit unless we run
# something that continues to execute. We'll use tail to to monitor
# webserver accesses.
#
CMD	/usr/sbin/nginx -c /etc/nginx/nginx.conf && \
	tail -f /var/log/nginx/access.log






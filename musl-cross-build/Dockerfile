FROM alpine:3.16.2

# Load the script
COPY build.sh .

# Install the dependencies
RUN apk update && apk add make g++ python3 gnupg curl file flex patch rsync texinfo

# Build the musl image
RUN chmod a+x build.sh && ./build.sh

# Remove our script that we don't need
RUN rm -rf build.sh

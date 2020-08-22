# Prepare the build image
FROM alpine:latest AS BUILD_IMAGE

# Install depedencies
RUN apk add --no-cache cmake gcc git libc-dev make

# Clone, build, and install wla-dx
RUN git clone https://github.com/vhelin/wla-dx
RUN mkdir -p /wla-dx/build
    
WORKDIR /wla-dx/build

RUN cmake .. && \
    cmake --build . --config Release && \
    cmake -P cmake_install.cmake

# Prepare the final image
FROM alpine:latest

# Install make
RUN apk add --no-cache make

# Copy the binaries we need
COPY --from=BUILD_IMAGE /usr/local/bin/wla-z80 /usr/local/bin/wla-z80
COPY --from=BUILD_IMAGE /usr/local/bin/wlalink /usr/local/bin/wlalink

# Set the working directory
WORKDIR /home
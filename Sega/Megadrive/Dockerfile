# Prepare the build image
FROM alpine:latest AS BUILD_IMAGE

# Install depedencies
RUN apk add --no-cache gcc libc-dev make g++ tar wget

# Clone, build, and install wla-dx
RUN wget http://phoenix.owl.de/tags/vasm1_8h.tar.gz
RUN tar -xf vasm1_8h.tar.gz

WORKDIR /vasm

RUN make CPU=m68k SYNTAX=mot

# Prepare the final image
FROM alpine:latest

# Install make
RUN apk add --no-cache make

# Copy the binaries we need
COPY --from=BUILD_IMAGE /vasm/vasmm68k_mot /usr/local/bin/vasmm68k_mot

# Set the working directory
WORKDIR /home
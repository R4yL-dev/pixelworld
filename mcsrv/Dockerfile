FROM debian:12.9

WORKDIR /opt/mcsrv

RUN apt update && apt install -y \
	openjdk-17-jdk \
	wget \
	&& apt clean && rm -fr /var/lib/apt/lists/*

# Download and setup mc server
RUN wget https://piston-data.mojang.com/v1/objects/5b868151bd02b41319f54c8d4061b8cae84e665c/server.jar \
	&& echo "eula=true" > eula.txt

# Download and setup forge
RUN wget https://maven.minecraftforge.net/net/minecraftforge/forge/1.20.2-48.1.0/forge-1.20.2-48.1.0-installer.jar \
	&& java -jar forge-1.20.2-48.1.0-installer.jar --installServer \
	&& rm forge-1.20.2-48.1.0-installer.jar

# Download Pixermon
RUN wget -P ./mods/ https://dl.reforged.gg/3Vz90yB \
	&& mv ./mods/3Vz90yB ./mods/Pixelmon-1.20.2-9.2.10-universal.jar

# Create the service user
RUN useradd -m -d /opt/mcsrv -s /bin/bash mcadmin \
	&& chown -R mcadmin:mcadmin /opt/mcsrv

USER mcadmin

EXPOSE 25565

CMD ["./run.sh", "nogui"]

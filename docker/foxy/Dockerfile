# Dockerfile with how2flow/config:{tag}

# ===== No Edit =====
FROM how2flow/config:{distro}
# ===================

# ===== Edit you want =====
ENV ID="ros2foxy"
  PASSWORD="docker"
# =========================

# ===== No Edit =====
USER root
WORKDIR /root
COPY fixups fixups
RUN chmod -R +x fixups
RUN ./fixups/postfix $ID $PASSWORD
# ===================

# TODO in /root ...
COPY preinst preinst
COPY packages packages
RUN chmod +x preinst packages && \
  ./preinst && rm preinst && \
  ./packages && rm packages

# ===== No Edit =====
RUN rm -rf fixups
# ===================

# ===== No Edit =====
USER ${ID}
WORKDIR /home/${ID}
RUN vim +PluginInstall +qall
# ===================

# TODO in /home/${ID} ...
COPY postinst postinst
RUN echo $PASSWORD | sudo -S chmod +x postinst && \
  ./postinst && rm postinst

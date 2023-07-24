# Dockerfile with how2flow/config:{tag}

# ===== No Edit =====
FROM how2flow/config:focal
# ===================

# ===== Edit you want =====
ENV ID="ros2foxy" \
  PASSWORD="docker"
# =========================

# ===== No Edit =====
USER root
RUN /postfix.sh $ID $PASSWORD
# ===================

# TODO with root permission ...
ADD preinst /
ADD packages /
RUN chmod +x /preinst /packages && \
  /preinst && rm /preinst && \
  /packages && rm /packages

# ===== No Edit =====
RUN rm -f /*.sh
# ===================

# ===== No Edit =====
USER ${ID}
WORKDIR /home/${ID}
RUN vim +PluginInstall +qall
# ===================

# TODO with normal permission in /home/${ID} ...
ADD postinst /
RUN echo $PASSWORD | sudo -S chmod +x /postinst && \
  /postinst && rm /postinst

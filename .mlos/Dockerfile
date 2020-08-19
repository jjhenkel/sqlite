FROM findtune/builder-base

# Copy target into container
COPY . /app/

RUN apt-get update && apt-get install -y tcl

# Specify build/configure and plugin activation point
RUN {                                      \
  echo '#!/bin/bash';                      \
  echo '/app/configure';                   \
  echo 'touch -d "$(date -R -r /app/Makefile.linux-gcc)" /app/Makefile.in' \
  echo 'export META_PLUGIN_ACTIVATED="Y"'; \
  echo 'make -j$(nproc)';                  \
} > /mlos-build.sh \
  && chmod +x /mlos-build.sh

# Entrypoint runs build w/ plugin active
ENTRYPOINT [ "/mlos-build.sh" ]

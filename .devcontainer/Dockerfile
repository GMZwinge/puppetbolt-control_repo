FROM puppet/pdk:latest

# [Optional] Uncomment this section to install additional packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get --yes install --no-install-recommends <your-package-list-here>

#
# Remove when [Install build essentials and Puppet Bolt](https://github.com/puppetlabs/pdk-docker/pull/72) is merged and image published:
RUN apt-get update \
    #
    # To build Gem native extension:
    && apt-get install --yes build-essential \
    #
    # Install Puppet Bolt.
    && pdk_ruby_bindir="$(dirname "$(ls -dr /opt/puppetlabs/pdk/private/ruby/*/bin/gem | head -1)")" \
    && "${pdk_ruby_bindir}/gem" install --no-document bolt --version '3.30.0' \
    && ln -s "${pdk_ruby_bindir}/bolt" /usr/local/bin/bolt

# Avoid this warning:
#   Project directory '/workspaces/puppetbolt-control_repo' is world-writable which poses a security risk.
#   Set BOLT_PROJECT='/workspaces/puppetbolt-control_repo' to force the use of this project directory.
ENV BOLT_PROJECT='/workspaces/puppetbolt-control_repo'

# General-purpose Ruby Docker Image

## Description

Creates a Docker image with Ruby, rubygems and bundler.

Before you go building 2.0.0-p247, you can already use my image by
running:

    docker pull binaryphile/ruby:2.0.0-p247

Also, before you ask where the Dockerfile is, there isn't one.
`dockerfile.sh` is a shell script which performs the steps that a
Dockerfile would, which is why it is named that way.

The image is meant to be reusable, so you should only need to build a
new image if you need a version of ruby other than 2.0.0-p247, otherwise
you should just use mine.

## Usage

- Copy `sample.env` to `.env`
- Edit `.env` and set:
  - **RUBY_VERSION**: the version of Ruby you want to install including
  patch level, e.g. 2.0.0-p247
  - **RI_VERSION**: the version of [ruby-install] to use
- run `./dockerfile` and wait for it to finish
- determine the id of the finished container with `docker ps -l` (use
sudo if need be)
- (optional) commit the image: `docker commit [id]
[your-index-name]/[your-repo-name][:optional tag]`
- (optional) push your image: `docker push
[your-index-name]/[your-repo-name]`

## Contents

The resulting image will contain a ruby interpreter installed in
`/usr/local` that will be on your regular path, so you'll have access to
ruby, gem, etc.  If you are running bundler as a regular user, you'll
want to pass it the `--path [pathname]` option to tell it not to use the
system gems, since they'll fail when running as a regular user.

[ruby-install]: https://github.com/postmodern/ruby-install


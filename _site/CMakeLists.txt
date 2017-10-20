cmake_minimum_required(VERSION 3.8)
project(gilescope_github_io)

set(CMAKE_CXX_STANDARD 11)

set(SOURCE_FILES
        _posts/2017-10-14-The-Quickening.markdown
        _posts/2017-10-15-welcome-to-jekyll.markdown
        _posts/temp.txt
        404.html
        _config.yml
        about.md
        Gemfile
        Gemfile.lock
        index.md)

add_executable(gilescope_github_io ${SOURCE_FILES})
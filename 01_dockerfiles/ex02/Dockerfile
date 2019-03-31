FROM ruby

RUN apt-get update && apt-get -y upgrade && \
	apt-get install -y nodejs

ONBUILD COPY app /opt/app
ONBUILD WORKDIR /opt/app

ONBUILD EXPOSE 3000
ONBUILD RUN bundle install
ONBUILD RUN rake db:migrate
ONBUILD RUN rake db:seed

# 1) docker build -t ft-rails:on-build .

# 2) git clone a ruby test app from:
# https://bitbucket.org/railstutorial/sample_app_4th_ed.git
# or https://github.com/RailsApps/rails-signup-thankyou

# 3) modify the sample_app's Gemfile.lock:
# rake (12.3.1) -> rake (12.3.2)

# 4) Go into git repo for ruby app and create a Dockerfile, 
# copy-paste from below:

## FROM ft-rails:on-build

## EXPOSE 3000
## CMD ["rails", "s", "-b", “0.0.0.0”, “-p”, "3000"]

# 5) build it:
# cd ../ (out of sample_app, and back to ex02)
# docker build -t ex02 .
# docker run -it --rm -p 3000:3000 ex02

# 6) Example ruby instructions:
# print "Hello Ruby!\n"
# 40 + 2
# etc...
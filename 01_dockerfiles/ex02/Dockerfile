FROM ruby

RUN apt-get update && apt-get -y upgrade && \
	apt-get install -y nodejs

ONBUILD COPY app /opt/app
ONBUILD WORKDIR /opt/app

ONBUILD EXPOSE 3000
ONBUILD RUN bundle install
ONBUILD RUN rake db:migrate
ONBUILD RUN rake db:seed

# docker build -t ft-rails:on-build .

# test app: https://bitbucket.org/railstutorial/sample_app_4th_ed.git
# or https://github.com/RailsApps/rails-signup-thankyou
# modify app/Gemfile.lock:
# rake (12.3.1) -> rake (12.3.2)

# FROM ft-rails:on-build

# EXPOSE 3000
# CMD ["rails", "s", "-b", “0.0.0.0”, “-p”, "3000"]

# docker build -t ex02 .
# docker run -it --rm -p 3000:3000 ex02

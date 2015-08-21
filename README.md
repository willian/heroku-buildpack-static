# Heroku Buildpack for Static HTML Websites

This buildpack will work out of the box with static files. It installs Nginx.

## Usage

Creating a new Heroku instance from you project's parent directory:

```
$ heroku create --buildpack https://github.com/willian/heroku-buildpack-static.git

$ git push heroku master
...
-----> Heroku receiving push
-----> Fetching custom buildpack
...
```

Or, use the Heroku Deploy button:

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)

## Configuration

You can set a few different environment variables to turn on features in this buildpack.

### Nginx Workers

Set the number of workers for Nginx (Default: `4`):

```
$ heroku config:set NGINX_WORKERS=4
```

This will depend on your Heroku instance size and the amount of dynos.

### Authentication

Setting `BASIC_AUTH_USER` and `BASIC_AUTH_PASSWORD` in your Heroku application will activate basic authentication:

```
$ heroku config:set BASIC_AUTH_USER=EXAMPLE_USER
$ heroku config:set BASIC_AUTH_PASSWORD=EXAMPLE_PASSWORD
```

*Be sure to use HTTPS for added security.*

### Force HTTPS/SSL

It supports the headers `X-Forwarded-Proto` ([used by Heroku](https://devcenter.heroku.com/articles/http-routing#heroku-headers)) and `CF-Visitor` ([used by CloudFlare](https://support.cloudflare.com/hc/en-us/articles/200170536-How-do-I-redirect-HTTPS-traffic-with-Flexible-SSL-and-Apache-)). Enable this feature in Nginx by setting `FORCE_HTTPS`:

```
$ heroku config:set FORCE_HTTPS=true
```

### Naked Domain Redirection

Visitors can be redirected from your "naked domain" (`example.com`) to `www.example.com`. Set your naked domain:

```
$ heroku config:set NAKED_DOMAIN=example.com
```

*This uses a HTTP 301 redirect to forward the request. All parameters are preserved.*

### Custom Nginx

In your project, add a `config/nginx.conf.erb` file and add your own Nginx configuration.

*You should copy the existing configuration file in this repo and make changes to it for best results.*

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

*This buildpack is based on [tonycoco/heroku-buildpack-ember-cli](https://github.com/tonycoco/heroku-buildpack-ember-cli) without Ember's needs*

# Adding a custom domain name

## Find a domain name that you want
Use [instant domain search](https://instantdomainsearch.com) to find out whether your desired domain names are available.

## Buy yourself a domain name
I use [Gandi](https://www.gandi.net/), but you can use whatever service you like to purchase a domain name. There isn't anything complicated to it. You select what you want (probably just the `.com` version), pay, and bam, you own that domain name.

## Deploy a working heroku app
If you need help with this, follow the instructions we've provided before for [rails apps](https://github.com/SF-WDI-LABS/shared_modules/blob/master/how-to/deploy-rails-to-heroku.md) or [MEAN stack apps](https://github.com/SF-WDI-LABS/shared_modules/blob/master/how-to/heroku-mean-stack-deploy.md).

## Sign up for a [CloudFlare](https://www.cloudflare.com/) account and add a site
CloudFlare is a service that stands as a layer between the browser and the server that serves up your site. It provides some security and protection and can make your app load faster for your users. CloudFlare also provides data about the performance of your site and helps you avoid crashes by caching working copies of your site. We're going to use it to make sure that our domain names are all squared away.

Once you make an account on [CloudFlare](https://www.cloudflare.com/) click "Add Site" in the top bar of the page. Type in the domain name you just purchased and press "Begin Scan." It should look like this:

![](https://cloud.githubusercontent.com/assets/6520345/15349305/abcf7714-1c86-11e6-9998-20252f1d915a.png)

Once that loader bar completes, it should look like:

![](https://cloud.githubusercontent.com/assets/6520345/15349326/d289df0c-1c86-11e6-987d-4cafe761b985.png)

Click continue setup to...

## Continue setup

You'll find yourself on a screen that looks like:

![](https://cloud.githubusercontent.com/assets/6520345/15349384/39272c38-1c87-11e6-8ae7-c450abf42e39.png)


We'll be coming back there in a moment, but for now, just hit the confirm button on that page to move onto a page that allows you to select a plan. Select the free plan:

![](https://cloud.githubusercontent.com/assets/6520345/15349921/062f9b40-1c8b-11e6-8d2f-9772cfccfbc3.png)

## Change Your Nameservers
Next you'll see a screen that looks something like this:

![](https://cloud.githubusercontent.com/assets/6520345/15349941/27714c54-1c8b-11e6-8db3-a90d85c89915.png)

You're going to need to go back to the place where you purchased your domain name and change the nameservers to match what CloudFlare has specified here.

On Gandi, you'll go to the dashboard for your domain name, where you'll see this in the bottom right:

![](https://cloud.githubusercontent.com/assets/6520345/15349985/680e51f8-1c8b-11e6-9c7a-54332a24b8a6.png)

Choose modify servers and this screen will appear:

![](https://cloud.githubusercontent.com/assets/6520345/15350033/bad7801c-1c8b-11e6-801a-24b1a5dca387.png)

Make the edits that CloudFlare specified.

Once you've done that, you can return to your CloudFlare dashboard and hit the Recheck Nameservers button:

![](https://cloud.githubusercontent.com/assets/6520345/15350058/f72fe5e0-1c8b-11e6-8a57-b513388ea25d.png)

## Add the proper DNS records

Return to the page that looks like this:

![](https://cloud.githubusercontent.com/assets/6520345/15349384/39272c38-1c87-11e6-8ae7-c450abf42e39.png)

It probably will no longer have the message "Verify..." at the top.

You can simply hit all of the x boxes to the right of each of those DNS records because we won't be using them.

Instead add a CNAME with your domain name (ex: `ostrichjoust.com`) and the IPv4 address as the heroku app that you have deployed (ex: `immense-retreat-30673.herokuapp.com`). **NOTE: Make sure that you do not include the leading `http://` or any trailing `/`'s or you may have some trouble**.

You can also add a CNAME with `www` and the IPv4 address as your heroku app. Overall, your two DNS records will look like so:

![](https://cloud.githubusercontent.com/assets/6520345/15350206/caac881a-1c8c-11e6-9a9c-19d4c4d409c0.png).

## Register your new domain names with Heroku

We're nearly there and we can check that our custom domain name is doing something different now. Unfortunately, that something different is the classic heroku error:

![](https://support.dnsimple.com/files/dnsimple-heroku-nosuchapp.png)

So, we need to tell Heroku that we want to use this custom domain name. For this app, go to Settings and scroll down to Domains.

![](https://cloud.githubusercontent.com/assets/6520345/15350260/392e31ee-1c8d-11e6-8501-ea11b8e18ef1.png)

Simply hit that add domain button and add your custom domain:

![](https://cloud.githubusercontent.com/assets/6520345/15350281/560e1c3e-1c8d-11e6-95ab-6d45400715b7.png)

You'll also probably want to add the domain name with the leading `www.` so that your final domain name section on heroku will look like:

![](https://cloud.githubusercontent.com/assets/6520345/15350315/8325c5a0-1c8d-11e6-81e5-9bd056da550f.png)

Once you've saved this all should be well! Try reloading your custom domain to see what happens!

## Troubleshooting

Some of these changes can take a while to come into effect! Some stages could take up to 24 hours to come into effect. If you get stuck with this problem, take a few hours off, reload, and see if it's magically working. If not, circle back and troubleshoot.

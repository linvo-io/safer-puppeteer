
[Puppeteer](https://github.com/puppeteer/puppeteer)  is one of the leading tools for automating browsers.  
Check out also  [Selenium](https://www.selenium.dev/) and [Cypress](https://www.cypress.io/).

This article assumes you have already worked with Puppeteer before.

Puppeteer is great for E2E testing but, when it comes to scarping / automation, there are few things we need to do.

So let’s start from the basics.

1).  **User-Agent:**

By default your Puppeteer User-Agent is

**“Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) HeadlessChrome/79.0.3945.0 Safari/537.36”**

You can understand that:  **This is headless chrome on Linux.**

Make sure you change it to something closer to:

**“‘Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36′”.**

**2). Using a proxy:**

By default, Puppeteer allows you to proxy your entire browser.  
That isn’t good because we don’t want to open a new browser for every task.

In case you want to proxy a single web page, you can check  [puppeteer-page-proxy](https://github.com/Cuadrix/puppeteer-page-proxy).  
It has problems with Content Security Policy, and I don’t really find it safe.

We don’t want to open a new browser for every task (it will consume all your memory).

We need to use a backbone network.

**What is a backbone network?**

You can look at it as a proxy for proxies.

You have one web-address.  
When you proxy this address, it will ask you for a username and password.

According to your username and password it will forward your request to a different IP.

Your Puppeteer launch should look like this:

**puppeteer.launch({**

**headless: true,**

**args: [**

**“–proxy-server=http://proxy-backbone.server”,**

**]**

**});**

After you open a new page, you should write:

**page.authenticate({**

**username: ‘username’,**

**password: ‘password’**

**});**

In case you want to manage your proxies yourself, check  [Apify](https://apify.com/)  library  [proxy-chain](https://github.com/apify/proxy-chain).

If your automation is done via a simple HTTP website (not SSL), check out  [Nikolai Tschacher tutorial about proxies.](https://incolumitas.com/2020/02/14/dynamically-changing-puppeteer-http-proxy/)

We are currently using  [Webshare.io](https://webshare.io/).  
Check out also [PrivateProxy.me](https://privateproxy.me/).

  

3).  **Libraries that will boost-up your safety**

**[Puppeteer-extra](https://www.npmjs.com/package/puppeteer-extra)** is an excellent extension Library for Puppeteer**.**

You can use it with **[puppeteer-extra-plugin-stealth](https://github.com/berstend/puppeteer-extra/tree/8d10f555c0af4ea206c9bab4439e93ccbba8dc40/packages/puppeteer-extra-plugin-stealth),**

They solve the **[Mouse & Cat problem](https://github.com/paulirish/headless-cat-n-mouse).**

Also, make sure you use  [puppeteer-extra-plugin-minmax](https://www.npmjs.com/package/puppeteer-extra)**.**  
**It just another thing to make your behavior looks more natural.**

4).  **Use more of Puppeteer native clicks and typing.**  
Try to avoid  **page.evaluate**  to make actions.  
Clicking on Elements without Puppeteer is inhuman, which might be detectable.

5). **Try to avoid patterns**

Don’t scrape a website every X seconds, do it more randomly.

Change your actions steps in every try to make it looks more random.

6). **Make sure you don’t modify the elements on the page.**

The article can be found at [Linvo.io](https://linvo.io/2020/12/06/how-to-make-your-puppeteer-safer/)

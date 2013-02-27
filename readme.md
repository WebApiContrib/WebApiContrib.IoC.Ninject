# WebApiContrib.IoC.Ninject

## Getting Started

If you would like to use [Ninject](http://www.ninject.org/) as your Inversion of Control Container inside your ASP.NET Web API application, this library will make things simple. Here are the steps to getting started on a new project with [WebApiContrib.IoC.Ninject](/).

***1. Create new project***

After you create a new project, you'll have your standard application setup in `Global.asax.cs`:

    protected void Application_Start()
    {
        AreaRegistration.RegisterAllAreas();

        WebApiConfig.Register(GlobalConfiguration.Configuration, ninjectResolver);
        FilterConfig.RegisterGlobalFilters(GlobalFilters.Filters);
        RouteConfig.RegisterRoutes(RouteTable.Routes);
        BundleConfig.RegisterBundles(BundleTable.Bundles);
    }

***2. Add a Reference***

The best way to get your hands on [WebApiContrib.IoC.Ninject](/) is to grab the package from NuGet:

    Install-Package WebApiContrib.IoC.Ninject

***3. Tying it Together***

You're now ready to bring it all together. Here's what a sample application might look like after we've added Ninject.

    protected void Application_Start()
    {
        AreaRegistration.RegisterAllAreas();

        var config = GlobalConfiguration.Configuration;

        IKernel kernel = new StandardKernel();
        kernel.Bind<IMessageSender>().ToConstant(new HardCodedMessageSender());

        // NOTE: Ensure you're using System.Web.Http.Dependencies.IDependencyResolver
        System.Web.Http.Dependencies.IDependencyResolver ninjectResolver = new NinjectResolver(kernel);
        config.DependencyResolver = ninjectResolver;

        WebApiConfig.Register(config);
        FilterConfig.RegisterGlobalFilters(GlobalFilters.Filters);
        RouteConfig.RegisterRoutes(RouteTable.Routes);
        BundleConfig.RegisterBundles(BundleTable.Bundles);
    }

***4. That's It!***

Fairly simple, right? After bringing this code into your project, you can now leverage all the benefits and goodness that Ninject has to offer. Happy building!

## Help! - Issues, Questions, and Anything Else

If you're in need of any assistance, your fastest method to get in touch with somebody that might be able to help is through the WebApiContrib mailing list: https://groups.google.com/group/webapicontrib

Another great way is to [leave an issue](https://github.com/WebApiContrib/WebApiContrib.IoC.Ninject/issues) on the GitHub repository.

For Ninject specific questions, please see the [Ninject documentation](http://www.ninject.org/learn).

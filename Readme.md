How to install
==============
  Add the following lines to your deps file:
      
    [ITZRouterBundle]    
        git=http://github.com/imikay/RouterBundle.git
        target=/bundles/ITZ/RouterBundle

  Run the command:
    
    php bin/vendors install

  Add the following two lines to your parameters.ini(in app/config folder)  

    router.options.generator_base_class = ITZ\RouterBundle\Component\Routing\Generator\UrlGenerator
    router.options.matcher_dumper_class = ITZ\RouterBundle\Component\Routing\Matcher\Dumper\PhpMatcherDumper
      
  Add one method - getParent to you bundle to make your bundle inherit from Symfony FrameworkBundle, for example

    <?php
        # src/Acme/DemoBundle/AcmeDemoBundle.php

        namespace Acme\DemoBundle;

        use Symfony\Component\HttpKernel\Bundle\Bundle;

        class AcmeDemoBundle extends Bundle
        {
            public function getParent()
            {
              return 'FrameworkBundle';
            }
        }
  
  You are done.
    
Quick example
=============

	_some_route:
		pattern:   /something/{slug}
		defaults: { _controller: AcmeDemoBundle:Something:something }
		requirements:
		  _host: http://{subdomain}.example.com
		  subdomain: /^option1|option2$/
		  _scheme: http

  or

    /**
     * @Route("/something/something", name="_some_route",  requirements = {"_host" = "subdomain.example.com" })
     * @Template()
     */
    public function somethingAction()
    {
        return array();
    }


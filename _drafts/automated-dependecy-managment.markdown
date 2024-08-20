<style type="text/css">
	.twitter-tweet {
		margin-left: auto;
		margin-right: auto;
	}
</style>

# Automated Dependency Management Considered Harmful

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">This applies equally to any dependency manager, any platform, it&#39;s a systemic issue, not a critique of any one system (i.e. if you are a partisans and thinks your system is better, it&#39;s not, they are equivalent in their defects)</p>&mdash; iStumbler Labs (@istumbler) <a href="https://twitter.com/istumbler/status/1273300794490548225?ref_src=twsrc%5Etfw">June 17, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

TL;DR: You cannot depend on a dependency manager. You should not be using a dependency manager to manage your apps dependencies. The hard part of managing dependencies is not resolving the dependency graph, it's resisting the temptation to use so many libraries.

## Automatic Dependency Management is Broken by Design

First things first: all automated dependency managers - which resolve a graph of dependencies and versions to compute a set of appropriate components for an app - have the same set of problems, and they all result from the primary features of the system: making it easy to add libraries to your app.

I'm not picking on your favorite dependency manager, which you think is super convenient; I'm pointing out that the entire category is fatally flawed and should be considered harmful to serious software engineers.

## Automated Dependency Management ≠ Configuration Management 

Once your system is so complex that you cannot manually manage all the dependencies in it, you are in need of proper Configuration Management (CM). CM was developed to help manage production of complex items in factories; the configuration for an assembly line and it's associated build process are concepts which were carried over into the software engineering world as computer  programs, both the software itself and the associated process which manages the production and maintenance of that software - another concept borrowed from the manufacturing industry - grew in size.

A lot of dependency managers provide lock-files to provide some level of Configuration Management 

## Sounds Old Fashioned and Not Extremely Agile

Sure, it's not Agile. Agile was designed to produce web site font end content quickly, it's very useful in that context and is a great way for small teams to get from zero to minimum viable project. (Side note: If you know of a way to scale it to large, long term complex multi-platform and heterogeneous projects, please let me know, there is a large market for that.)

### But I neeeeeed all those frameworks

Here we come to the core of the problem, as in manufacturing "the best part is no part"; in software, the profligate use of 3rd party libraries, typically Free Open Source Software, bloats download size, drags out startup times, and can potentially add undesirable features such as location telemetry and introduce other privacy concerns. Additionally, because there are numerous different Open Source licenses, you will need a compliance plan to make sure you are correctly complying with and acknowledging them as required.

## Dependencies Create Hidden Risk

Frameworks can get big, they can get complex, they are in some cases are created by large distributed projects with numerous contributors and often unpaid volunteer maintainers and authors.

## Enables & Encourages Bad Practices


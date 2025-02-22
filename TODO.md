Main features which I still plan to support (before getting into actual code generation):

* Subcomponents (in progress)
	* Ensure that scopes defined in component bindings match with the component's scope. If the component doesn't have any scope, then it shall not allow any scoped bindings!
	* Make checking of all current possible errors more robust, make them halt the build process returning `false` back from the root parser build call to the plugin's '_build()' method that halts execution.
	* Extensively document everything implemented so far for easier future understanding.
	* Before implementing support for the 'assisted injection', 'binding instances' and 'qualifier' features, experiment with visual feedback on the dependency graph parsing process (including display errors visually).
* Component/Subcomponent Builders!
* Binds annotation - simply as a shortcut to provision methods that generates code on behalf of the user.
* Assisted injection - might be possible and simpler than in Dagger2, with factory classes being 100% generated for the user. The biggest challenge is how to let users annotate that certain constructor arguments are @assisted. The only viable solution I can think of right now is to let users optionally define a `GodDaggerAssistedInjection` argument indicating that the following arguments in the constructor are all assisted by the user.
* Binding instances - I'll need to add Builder support to components first (for overriding module instances), otherwise this doesn't make sense. Which means adding Builder and the create() convenience method (that instantiates modules on behalf of the user). Then I can work on letting users bind instances to the graph.


Features which might still be supported as well:
* Qualifiers? Will be supported by letting users pass subtypes of `GodDaggerQualifier` in the argument list, with the semantics that each qualifier instance affects the following dependency in the argument list. This is very similar to how Scopes were supported. The only problem is how to inform which qualified dependency is desired at injection site. If the order of properties is kept when parsing through the component's property list, I could perhaps let users specify a property right before the dependency declaration property with the same semantics that that's the qualified version desired. If this feature is implemented, it should also work for binding instances too.


Features which will not be supported:
* Multibindings
* Producers

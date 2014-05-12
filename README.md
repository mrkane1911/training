# AngularJS Training

From my research, tutorials, training videos etc. The list below is a pretty good take on what you should focus on when going through AngularJS. I have also included some resources below the list.


* Introduction to Single-Page-Apps, and how they contrast with traditional server centric web apps
* Where is AngularJS a good fit? Where is it not a good fit?
* Bindings: declarative connections between data and on-screen elements
* Controllers
* Scopes, including Root Scope and Isolated Scopes
* Scope should hold the model, not be the model
* Routing
* Using and writing filters
* Forms and validation
* Organizing your code with modules; how AngularJS modules compare with other module systems
* Dependency injection
* Services and Factories
* Directives: extending HTML to create abstractions for your application
* Events and event propagation
* Unit Testing with Jasmine and Karma
* End to end testing with Protractor
* Promises, and their pervasive use
* Batarang Debug Tool
* Alternate HTML syntax (Jade)
* Misc. AngularJS Topics


* Interacting with a backend / server with $http and Restangular
* build a small, real application




## Resources

[http://www.lynda.com/AngularJS-tutorials/Up-Running-AngularJS/154414-2.html](http://www.lynda.com/AngularJS-tutorials/Up-Running-AngularJS/154414-2.html)

Access above through people portal, search for Lynda.com and you can login through the Sapient account if you haven’t done so in the past. 

### The two below are just two quick tutorials to get you going.

[http://www.revillweb.com/tutorials/angularjs-in-30-minutes-angularjs-tutorial/](http://www.revillweb.com/tutorials/angularjs-in-30-minutes-angularjs-tutorial/)

[http://code.tutsplus.com/tutorials/building-a-web-app-from-scratch-in-angularjs--net-32944](http://code.tutsplus.com/tutorials/building-a-web-app-from-scratch-in-angularjs--net-32944)


  





##Tutorial

#### Structure of an application using Angular JS 
[See it in Action](http://cdpn.io/cdACy)

An application using Angular JS must have following components:

1. Reference to Angular JS library
2. A JavaScript controller containing data or with logic to fetch data


We have to add the [ng-app](http://docs.angularjs.org/api/ng.directive:ngApp) declaration to a portion of the page that uses features of Angular JS. It can be added to a div inside a page wherein we have to use some expressions of Angular JS. If it is needed for the entire page, we have to add the ng-app declaration to the body tag.

	
	<div ng-app>
	 <!-- Your markup goes here -->
	</div>

####A demo showing some data binding features of Angular JS

Let’s create a shopping cart. We will add the features to calculate total price of the cart, adding items to cart and removing items from cart. We have to add this logic to the controller. An Angular JS controller must follow the following conventions:

1. It should be a JavaScript function accepting an argument named $scope
2. All of the model variables and functions should be added to the $scope object
3. Controllers are usually suffixed with Ctrl, but it is not necessary


Following is the controller with the required functionalities added:

	
	function ShoppingCartCtrl($scope)  {
	    $scope.items = [
	        {Name: "Soap", Price: "25", Quantity: "10"},
	        {Name: "Shaving cream", Price: "50", Quantity: "15"},
	        {Name: "Shampoo", Price: "100", Quantity: "5"}
	    ];
	 
	    $scope.addItem = function(item) {
	        $scope.items.push(item);
	 $scope.item = {};
	    }
	     
	    $scope.totalPrice = function(){
	        var total = 0;
	 for(count=0;count<$scope.items.length;count++){
	     total += $scope.items[count].Price*$scope.items[count].Quantity;
	 }
	 return total;
	    }
	   
	    $scope.removeItem = function(index){
	        $scope.items.splice(index,1);
	    }
	}

To bind data using members of the controller, we have to specify the controller using [ng-controller](http://docs.angularjs.org/api/ng.directive:ngController) directive. Ensure that the element containing ng-controller directive is a child of an element declared as ng-app.

	
	<div ng-app>
	 	<div ng-controller="ShoppingCartCtrl">
	  		<!-- Your markup goes here -->
		</div>
	</div>

Let’s display the items added to items array in a table. Let’s also add a button on each row to remove the item. We have to use the following blocks to achieve this:

1. [ng-repeat](http://docs.angularjs.org/api/ng.directive:ngRepeat) directive to iterate through items
2. Binding controller’s properties using {{}}
3. [ng-click](http://docs.angularjs.org/api/ng.directive:ngClick) directive to bind button click event
4. $index to use current index in an array


Following is the table displaying items:
	
	<table border="1">
	 <thead>
		 <tr>
			<td>Name</td>
			<td>Price</td>
			<td>Quantity</td>
			<td>Remove Item</td>
		 </tr>
	 </thead>
	 <tbody>
		 <tr ng-repeat="item in items">
			  <td>{{item.Name}}</td>
			  <td>{{item.Price}}</td>
			  <td>{{item.Quantity}}</td>
			  <td><input type="button" value="Remove" ng-click="removeItem($index)" /></td>
		 </tr>
	 </tbody>
	</table>

Let’s display the total price of cart below this table. For this, we need to call the totalPrice() function of controller.

	
	<div>Total Price: {{totalPrice()}}</div>

Finally, let’s add a form to accept values from user and add the new item to items array. We have to use ng-model directive to automatically add an input field to a property of the controller. Following is the form:

	
	<table>
	 <tr>
	  <td>Name: </td>
	  <td><input type="text" ng-model="item.Name" /></td>
	 </tr>
	 <tr>
	  <td>Price: </td>
	  <td><input type="text" ng-model="item.Price" /></td>
	 </tr>
	 <tr>
	  <td>Quantity: </td>
	  <td><input type="text" ng-model="item.Quantity" /></td>
	 </tr>
	 <tr>
	  <td colspan="2"><input type="Button" value="Add" ng-click="addItem(item)" /> </td>   
	 </tr>
	</table>

When we enter something in the text boxes, a property named item is automatically added to $scope. This property is used in the addItem function. 

####You can play around with the finished app by [Clicking Here](http://cdpn.io/cdACy)

As we saw, two-way data binding is made very easy using directives and binding syntax of Angular JS. All we need is a controller with some members in it. We don’t need to invoke any special functions to send notification when something changes in the controller. Everything is available for free to us, all we need to do is follow the conventions. 

We will explore other features of Angular JS in future posts. 



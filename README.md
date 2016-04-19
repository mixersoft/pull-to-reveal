# directive:pullToReveal
A pull-to-reveal directive for Ionic Framework that was hacked from the `ion-refresher` directive. Hides content in the overscroll above `<ion-content>` until the user pulls down. Can also be manually triggered.

Place it as the first child of your `ionic.directive:ionContent` or
`ionic.directive:ionScroll` element.

When the reveal is complete the content remains visible in the scroll until hidden

```html
<ion-content overflow-scroll="true">
  <pull-to-reveal reveal="showOverscroll" on-pulled="onPulled()" style="height:115px;">
    <div class="card">
      <ion-item class="item-balanced" ng-click="onToggleReveal()"> pull-to-reveal (click to hide) </ion-item>
      <ion-item>
        Hello, I am hidden in the overscroll!
        <span style="color:red;">{{wasPulled ? "I was pulled to reveal" : "I was manually revealed"}}</span>
      </ion-item>
    </div>
  </pull-to-reveal>

  <div class="list">
    <ion-item ng-repeat="item in list">{{item}}</ion-item>
  </div>
</ion-content>
```
```js
angular.module('testApp', ['ionic'])
.controller('MainCtrl', function($scope) {
  // manually reveal by setting this value
  $scope.showOverscroll = false;
  $scope.wasPulled = null;
  $scope.onPulled = function(value) {
    $scope.wasPulled = true;
    $scope.showOverscroll = true;
  }
  $scope.onToggleReveal = function() {
    $scope.showOverscroll = !$scope.showOverscroll
    if ($scope.showOverscroll == false) {
      $scope.wasPulled = null
    }
  }
  $scope.list = [1,2,3,4,5]
});
```
## attributes
- {expression=} reveal, manually reveal/hide `pull-to-reveal`
- {expression&} on-reveal, Called when the `pull-to-reveal` is revealed
by a pull-down, i.e. touchend
- {expression&} on-refresh Called when the user pulls down enough and lets go
of `pull-to-reveal`.
- {expression&} on-pulling Called when the user starts to pull down
on `pull-to-reveal`.

##NOTES:
	- seems to only work with native scrolling, overflow-scroll="true"
	- give the pull-to-reveal element an explicit height via inline style attr

also, the child/transclude element can manually reveal/hide with
		`$scope.$emit('pullToReveal.reveal', [boolean])`

## Demo
see: http://codepen.io/anon/pen/aNKvWq

## Authentication & Authorisation4

## Authentication & Authorization | Part 4
* Integrating APIs
* Get Exclusive Prime Deals
* API Call Possible Views
* Handle Success View
* Handle Failure View
* Handle Loading View

## 1. Integrating APIs
*  Get Exclusive Prime Deals
Exclusive Prime deals are for Prime Users.
All Products are for both Prime and Non-Prime users.

## API Call Possible Views
# Success View
When the Prime User is logged in and accessed Prime Deals Section then we should show the Exclusive Prime Deals section.

## Failure View
When the Non-prime User is logged in and accessed Prime Deals Section then we should show the Get Exclusive Deals section.

## Reasons for API Call Failure :
Sending UnAuthorized User credentials
Not specifying Authorization header
Using the wrong HTTP method

## Loading View
When the Prime or Non-prime User is logged in and accessed Prime Deals Section, we should show the Loading view until data is in progress.

## Best Practices
# State Variable-isLoading

isLoading is used to handle Success View, Loading View only. 

render() {
   const {isLoading} = this.state
   return <>
   { isLoading ? this.renderLoader() : this.renderProductsList() }
   </>
 }
 -----------------------------------------------------------------------

 ##  State Variable-apiStatus
apiStatus is used to handle Success, Failure and Loading Views.


switch (apiStatus) {
  case apiStatusConstants.success:
    return this.renderPrimeDealsList()
  ...
  ...
  default:
    return null
}
------------------------------------------------------------------------

## Adding Initial State
Instead of adding empty strings in initial state we can add initial in apiStatusConstants.

## File: src/components/PrimeDealsSection/index.js

...
const apiStatusConstants = {
  initial: "INITIAL",
  inProgress: "IN_PROGRESS",
  success: "SUCCESS",
  failure: "FAILURE",
};
class PrimeDealsSection extends Component {
  state = {
    primeDeals: [],
    apiStatus: apiStatusConstants.initial,
  }

  renderPrimeDeals = () => {
    const { apiStatus } = this.state;
    switch (apiStatus) {
      case apiStatusConstants.success:
        return this.renderPrimeDealsSuccessView();
      case apiStatusConstants.failure:
        return this.renderPrimeDealsFailureView();
      case apiStatusConstants.inProgress:
        return this.renderLoader();
      default:
        return null;
    }
  };
  
  render() { 
      return <>{this.renderPrimeDeals()}</>
  }
 } 

export default PrimeDealsSection
------------------------------------------------------------------------

## Publish

https://handilingsfl.ccbp.tech
------------------------------------------------------------------------

//npm install --save react-router-dom@5.2.0
//
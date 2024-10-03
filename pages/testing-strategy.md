# Platform Experience Testing Strategy

JIRA: [RHCLOUD-31061](https://issues.redhat.com/browse/RHCLOUD-31061)

## Links

- [Tracking 2024 HCC UI efforts (Prod apps only)](https://docs.google.com/spreadsheets/d/10zYgnFTnUUwBhEpeAT1fgGZR-rNytcxrB_T9urZBjkM/edit#gid=0) \- **links to the IQE test repositories**  
- [Dev script for running IQE tests - lessons learned, potential pitfalls](https://docs.google.com/document/d/1E6_S4LT4XgTomlk9dGkNIywdJqzTaP60wlxbPaXNYjw/edit)  
- [https://spaces.redhat.com/display/INSIGHTSQA/Platform+Experience](https://spaces.redhat.com/display/INSIGHTSQA/Platform+Experience) (former QE docs)

## Test Coverage Levels

**Manual** \- Useful for one-off verifications that will NOT be repeated. For example, checking the content of strings on pages for spelling, verifying that an icon looks correct, or a visual inspection to confirm that spacing is correct are all examples of manual tests.

**Unit** \- Primarily owned by developers. Ensures that individual classes, functions, and more atomic components of the software operate correctly. UI developers are typically exposed to unit testing via framework documentation or via team-set standards for coverage and unit test coverage reporting. Typically unit tests are expected 100% in order to merge a change as part of PR gating.

**Functional** \- Functional testing ensures that a component made of many different pieces functions correctly in isolation. For example, an endpoint to GET RBAC roles can be functionally tested without having to interact with most of the other API endpoints. Functional tests can be covered either by UI engineers or by a framework like IQE in situations like API testing. Functional tests can be included as part of PR gating, and are in many cases for things like iqe-rbac-plugin (RBAC API).

**Integration** \- The term “integration testing” is an overloaded term used to describe component-level integration, functional component integration, end-to-end integration, and many other types of testing. It helps to be more specific about the kind of testing when referring to integration testing. 

- **Component Integration** \- One or more UI components or classes integrating with each other, typically including some form of mocking of external dependencies. Typically covered by developers as unit tests, but sometimes Quality Engineers will assist if there are concerns or questions about coverage. Sometimes these are mistaken for unit tests, although their scope of coverage is broader.  
- **Functional Integration \-** A great example of functional integration would be API tests that exercise the “workflow” of an API without the use of a UI. A test of this nature ensures that the API is functional without the burden of increasing the complexity and scope of the test to include the UI. Generally, pieces of functionality with a low degree of dependency on other parts of the system are good candidates for functional testing. Endpoints are one example. Another example is a small, partial UI flow such as a login page (user logs in, then verify that user lands on next page). Broadly speaking, functional testing should have a narrower scope than end-to-end coverage but it will include the integration of many different internal-only classes, and functions.  
- **E2E** \- In UI engineer parlance, e2e testing typically refers to end-to-end user flows coverage of a UI with either a mocked backend or a real back-end. Some UI frameworks have carefully dictated “e2e” use cases and patterns to follow to integrate with the UI frameworks (e.g. Angular). E2E testing falls into the scope of collaboration between developers and QEs.  
- **End-to-End User Flow Automated Testing \-** End to end user flow testing is the intended use case for the IQE framework. It encompasses the building of test automation that exercises the full range of functionality in the end-user’s flow with a fully-functional and operational supporting back-end. This is the most expensive type of integration testing to build, but it often “shakes out” broadly-scoped feature bugs or missed requirements from testing at more basic levels. This level of testing falls into the scope of collaboration between QEs and Developers, although the amount of expertise required to work with IQE typically makes this a primarily QE coding effort.

### Test Priority

End-to-End User Flow Automation is a necessity, but it is also the most expensive kind of testing to build. Consequently, we focus on two levels of priority in our testing:

**Critical Priority** \- A critical priority test covers a flow that *must work* lest the product/feature be rendered inoperable. 

* Example 1: An obvious of a Critical Priority test case is the user login flow. If the user login flow ceases to work, the user can’t log in, and the product is unusable by the end-user.   
* Example 2: For a feature, a critical test case would be an aspect of the feature that must work lest the feature be rendered unusable. For example, a critical feature of RBAC would be group edit/creation. If a user is unable to create or edit  an RBAC group, they would be unable to manage their users/permissions.

**High Priority** \- A high priority test case covers functionality that would have a high degree of impact to the end-user, but the feature/product is still usable via work-arounds or an impaired user experience. Emphasis on high-impact to user experience or the requirement of usage of work-arounds to maintain feature/product operability. 

* **Example 1**: For RBAC, a high priority fix would be the inability of an end-user to navigate to User Access via the provided UI links (links may be broken in this case). The user would have to work-around this issue via a bookmark or a direct link provided by engineering. The functionality is still available, but the use case is highly undesirable and would reflect poorly on Red Hat.

Note: Some organizations would consider certain UX-affecting issues to be Critical priority even if they don’t impair functionality. For example, a start-up whose logo is present, but has an incorrect copyright date or is stretched. To some degree, the difference between High and Critical is a fine line that is sometimes determined by stakeholders rather than by functional impairment.

### Release/Promotion Criteria

For a given feature or capability the following are typically mandatory to release or promote:

* Unit tests (100% passing)  
* Component Integration (100% passing)  
* Functional tests (if applicable)  
* End-to-End User Flow Automated Testing \- Critical and High priority tests must pass 100% to release to production (ideally) or QE go/no-go if tests are currently in an undesirable state. A small sampling of smoke tests run in certain pr\_checks for some UI repositories, but we’d like to expand this to be broader.

## HCC test account credentials

See [Test accounts credentials](https://docs.google.com/document/d/1-TYlSBHzfuPY-77hvMmP0zOXpDCfunLbD5xixUetv1g/edit?usp=sharing) \- [RHCLOUD-32948](https://issues.redhat.com/browse/RHCLOUD-32948)

## QE

- levels of testing QE work on (links to the tests)  
- IQE Navmazing/Widgetastic Tutorials  
    
- What are the preferred identifiers for QE to locate elements in DOM? Common format of OUIA IDs. Make sure identifiers are present where possible and changes do not break tests unexpectedly.

## 

## **React testing library guidelines**

* Any **React component** tested via Jest should be moved to a Cypress component test.   
* Use Jest only for unit testing of algorithms and hooks.

## **Cypress testing guidelines**

### Cypress HCC enablement specifics:

* example PR to set up Cypress on the Landing page [https://github.com/RedHatInsights/landing-page-frontend/pull/539](https://github.com/RedHatInsights/landing-page-frontend/pull/539) 

### Testing \- common:

* Finding elements  
  * **Do not use CSS selectors or Cpatch** to find elements, try to use the same tools a normal user would to find an element. **Use primarily text**, or use **ID or accessibility labels if there are conflicts** or other issues with obtaining the element via text.  
  * **If no good ID/label is present** on an element, **add it** to the source code.  
  * Using “internal” selectors like class names will become problematic specifically with PF or even internal styling updates. Users do not care if an element class is foo or bar as long as the element looks the same for them.

 

### Testing \- component:

* Tests components **parts of UI that are commonly used on many screens**. Historically we were writing tests in Jest. Any React component tested via **Jest should be moved to a Cypress component test**.   
* It is OK if there is some overlap with E2E tests, but E2E tests should not test all possibilities of a component.

### Testing \- E2E:

* 

## 

## **IQE Platform UI Plugin Overview**

Meeting recording: [https://drive.google.com/file/d/1lEhijwVpmJ8ky\_vNWLGJgrSHJBHtEGlV/view?usp=sharing](https://drive.google.com/file/d/1lEhijwVpmJ8ky_vNWLGJgrSHJBHtEGlV/view?usp=sharing)  
Basic structure:

- iqe\_platform\_ui  
  - /conf folder \- yaml configs (data and users definition \- pulled from vault in real time)  
  - /tests \- test files

Navmazing: 

- navigation management tool for automated testing \- facilitates navigation between different pages and ensures that the tests reach the goal based on the defined steps  
- each navigation step consists of two parts: the logic for navigation (**step**) and the check to ensure that the page was successfully reached (**is\_displayed**).   
- if navmazing encounters an issue (page not matching expectations), the navigation fails

pytest\_generate\_tests: [https://docs.pytest.org/en/7.1.x/how-to/parametrize.html](https://docs.pytest.org/en/7.1.x/how-to/parametrize.html)


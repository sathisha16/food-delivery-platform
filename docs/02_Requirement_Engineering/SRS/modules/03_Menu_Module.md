## 3.3 Menu Module

The Menu Module enables customers to explore restaurant menus, view food categories, access detailed item information, customize menu items, and make informed purchasing decisions before adding items to the shopping cart.

The functional requirements included in the Menu Module are:

### 3.3.1 View Menu

#### 3.3.1.1 Description

The **View Menu** functionality enables customers to browse the complete menu offered by a selected restaurant. After choosing a restaurant from the search results or restaurant listing, the customer shall be able to access its available menu items along with their categories, pricing, availability status, and other essential information required to make purchasing decisions.

The system shall retrieve the latest published menu from the restaurant and present it in an organized and user-friendly manner. Menu items shall be grouped into logical food categories such as Starters, Main Course, Beverages, Desserts, Breakfast, Lunch, Dinner, or any custom categories defined by the restaurant. Only menu items that are currently available for ordering shall be presented as available to the customer, while unavailable items shall be clearly identified.

The menu shall display sufficient information to help customers understand the available food options before viewing individual item details. Each menu item may include its name, price, short description, food type (Vegetarian, Non-Vegetarian, Vegan, Egg), availability status, estimated preparation time, rating, and thumbnail image where applicable.

The View Menu functionality shall provide a fast, consistent, and responsive browsing experience regardless of the number of menu items offered by the restaurant. The functionality shall ensure that customers always view the latest approved menu published by the restaurant while preventing access to unpublished, deleted, or restricted menu items.

#### 3.3.1.2 Actors

##### Primary Actor

- Customer

##### Supporting Actors

- Restaurant Service
- Menu Service
- Inventory Service
- Media Service
- Authentication Service (Optional, for authenticated customers)

#### 3.3.1.3 Preconditions

The following preconditions shall be satisfied before the customer can view a restaurant menu:

1. The restaurant shall exist in the system.

2. The restaurant shall be approved and active.

3. The restaurant shall have at least one published menu.

4. The menu shall be associated with the selected restaurant.

5. The customer shall have selected a restaurant from the search results, recommendations, favorites, or any other valid navigation flow.

6. The system shall be able to communicate successfully with the Menu Service.

7. The customer shall have network connectivity to retrieve the latest menu information.

8. The system shall verify that the requested restaurant is not permanently removed from the platform.

9. The menu data shall be available for retrieval.

10. Customer authentication shall not be mandatory for viewing a restaurant menu unless restricted by business policies.

#### 3.3.1.4 Trigger

The View Menu functionality shall be initiated when the customer selects a restaurant and requests to view its menu.

The functionality may be triggered through any of the following actions:

1. Selecting a restaurant from the restaurant listing.

2. Selecting a restaurant from the search results.

3. Selecting a restaurant from personalized recommendations.

4. Selecting a restaurant from the customer's favorite restaurants.

5. Selecting a restaurant from recent orders or order history.

6. Opening a restaurant through a shared restaurant link or promotional campaign.

Upon receiving the request, the system shall validate the restaurant and retrieve the latest published menu associated with the selected restaurant.

#### 3.3.1.5 Input Fields

| Field Name | Data Type | Mandatory | Description |
|------------|-----------|-----------|-------------|
| Restaurant ID | UUID / Integer | Yes | Unique identifier of the restaurant whose menu is requested. |
| Customer ID | UUID / Integer | No | Unique identifier of the authenticated customer. Used to personalize menu information such as favorites, recommendations, or applicable offers. |
| Location | Latitude & Longitude / Address | No | Customer's current delivery location used to verify restaurant serviceability and menu availability, if applicable. |
| Language Preference | String | No | Preferred language in which the menu content should be displayed, if multilingual support is available. |

#### 3.3.1.6 Business Rules

The following business rules shall govern the View Menu functionality:

1. The system shall display only the latest published menu associated with the selected restaurant.

2. The system shall display menu items only for restaurants that are approved and currently active on the platform.

3. The system shall organize menu items into their respective food categories as defined by the restaurant.

4. The system shall clearly indicate the availability status of each menu item.

5. Menu items that are temporarily unavailable shall remain visible to the customer but shall be clearly marked as unavailable and shall not be available for ordering.

6. Menu items that have been unpublished or permanently removed by the restaurant shall not be displayed to customers.

7. The system shall display the current selling price configured by the restaurant for each menu item.

8. The system shall display only menu items that comply with the customer's delivery location, where location-based menu restrictions are applicable.

9. The system shall ensure that menu information presented to the customer reflects the latest approved data available within the platform.

10. The system shall display food type indicators such as Vegetarian, Non-Vegetarian, Vegan, or Egg, where such information is provided by the restaurant.

11. The system shall display menu item images only when valid images are available.

12. The system shall allow customers to access detailed information for any displayed menu item.

13. Viewing a restaurant menu shall not require customer authentication unless restricted by applicable business policies.

14. The system shall record menu view activity for analytics, reporting, and recommendation purposes in accordance with applicable privacy policies.

15. The system shall ensure that only customers with appropriate access permissions can view menus that are restricted to specific customer groups or promotional campaigns, where applicable.

#### 3.3.1.7 Validations

The system shall perform the following validations before displaying the restaurant menu:

1. The system shall validate that the Restaurant ID is provided.

2. The system shall validate that the specified restaurant exists within the platform.

3. The system shall validate that the restaurant is approved and currently active.

4. The system shall validate that the restaurant is currently accepting customer orders, where applicable.

5. The system shall validate that at least one published menu exists for the selected restaurant.

6. The system shall validate that the published menu has not been deleted, archived, or disabled.

7. The system shall validate that the customer is authorized to access the requested menu if the menu is restricted to specific customer groups or promotional campaigns.

8. The system shall validate that menu data is successfully retrieved from the Menu Service.

9. The system shall validate that each menu item satisfies the visibility rules configured by the restaurant before displaying it to the customer.

10. The system shall validate the availability status of each menu item before presenting it for ordering.

11. The system shall validate the customer's delivery location against the restaurant's service area, where location-based menu visibility is applicable.

12. The system shall validate that all mandatory menu information required for customer viewing is available before displaying the menu.

#### 3.3.1.8 Main Flow

1. The customer selects a restaurant from the restaurant listing, search results, recommendations, favorites, order history, or any other valid navigation source.

2. The system receives the request to view the selected restaurant's menu.

3. The system validates the restaurant and verifies that it is active, approved, and eligible to accept customer requests.

4. The system retrieves the latest published menu associated with the selected restaurant.

5. The system retrieves all menu categories and their corresponding menu items.

6. The system validates the visibility and availability of each menu item before displaying it to the customer.

7. The system organizes the retrieved menu items under their respective food categories.

8. The system displays the restaurant menu along with the relevant information for each menu item, including item name, price, food type, availability status, short description, thumbnail image, and other applicable information.

9. The customer browses the available menu categories and menu items.

10. The customer may select any menu item to view its detailed information.

11. The system records the menu view activity for analytics and reporting purposes, where applicable.

12. The use case ends successfully after the restaurant menu is displayed to the customer.

#### 3.3.1.9 Alternate Flows

##### AF-1: Restaurant Does Not Exist

1. The customer requests to view a restaurant menu.
2. The system determines that the specified restaurant does not exist.
3. The system displays an appropriate error message indicating that the restaurant could not be found.
4. The use case ends.

---

##### AF-2: Restaurant Is Inactive or Not Approved

1. The customer requests to view a restaurant menu.
2. The system determines that the restaurant is inactive, suspended, or not approved.
3. The system denies access to the restaurant menu.
4. The system informs the customer that the restaurant is currently unavailable.
5. The use case ends.

---

##### AF-3: No Published Menu Available

1. The customer requests to view a restaurant menu.
2. The system determines that no published menu is available for the selected restaurant.
3. The system informs the customer that the menu is currently unavailable.
4. The use case ends.

---

##### AF-4: Restaurant Is Outside the Service Area

1. The customer requests to view a restaurant menu.
2. The system determines that the restaurant does not serve the customer's delivery location, where serviceability validation is applicable.
3. The system informs the customer that delivery is unavailable for the selected location.
4. The system may allow the customer to change the delivery location.
5. The use case continues after a valid delivery location is selected.

---

##### AF-5: Menu Service Is Unavailable

1. The customer requests to view a restaurant menu.
2. The system is unable to retrieve menu information due to a temporary service failure.
3. The system displays an appropriate error message.
4. The system may allow the customer to retry the request.
5. The use case ends.

---

##### AF-6: Customer Is Not Authorized to View the Menu

1. The customer requests to view a restricted restaurant menu.
2. The system determines that the customer does not satisfy the required access conditions.
3. The system denies access to the menu.
4. The system displays an appropriate authorization message.
5. The use case ends.

#### 3.3.1.10 Postconditions

Upon completion of the View Menu functionality, one of the following postconditions shall apply:

##### Successful Completion

1. The selected restaurant's latest published menu shall be displayed to the customer.

2. The customer shall be able to browse the available food categories and menu items.

3. The customer shall be able to proceed to view detailed information for any displayed menu item.

4. The system shall record the menu view activity for analytics, reporting, and recommendation purposes, where applicable.

5. The system shall maintain the customer's current browsing session for subsequent menu-related operations.

##### Unsuccessful Completion

1. The restaurant menu shall not be displayed.

2. The system shall notify the customer of the reason the request could not be completed.

3. No changes shall be made to the restaurant's menu data.

4. The system shall maintain data integrity and prevent the display of incomplete or unauthorized menu information.

#### 3.3.1.11 Success Response

Upon successful completion of the View Menu functionality, the system shall:

1. Display the latest published menu of the selected restaurant.

2. Display all available food categories associated with the restaurant.

3. Display the menu items under their respective food categories.

4. Display the current selling price for each menu item.

5. Display the food type of each menu item, where applicable (e.g., Vegetarian, Non-Vegetarian, Vegan, Egg).

6. Display the availability status of each menu item.

7. Display the menu item thumbnail image, where available.

8. Display a short description for each menu item, where provided.

9. Allow the customer to select any displayed menu item to view its complete details.

10. Present only the latest approved and published menu information available within the platform.

#### 3.3.1.12 Failure Response

If the View Menu functionality cannot be completed successfully, the system shall:

1. Inform the customer that the restaurant menu could not be displayed.

2. Display an appropriate and user-friendly message describing the reason for the failure, where applicable.

3. Prevent the display of incomplete, outdated, unpublished, or unauthorized menu information.

4. Allow the customer to retry the request if the failure is temporary.

5. Allow the customer to return to the restaurant listing or continue browsing other available restaurants.

6. Record the failure event for system monitoring, diagnostics, and auditing purposes, where applicable.

7. Ensure that no menu data is modified as a result of the failed request.

8. Maintain the customer's current session and application state unless termination is required due to security or system policies.

#### 3.3.1.13 Acceptance Criteria

The View Menu functionality shall be considered successfully implemented when all the following conditions are satisfied:

| AC ID | Acceptance Criteria |
|-------|----------------------|
| AC-VM-001 | The customer shall be able to view the latest published menu of the selected restaurant. |
| AC-VM-002 | The system shall display only menus belonging to approved and active restaurants. |
| AC-VM-003 | The system shall organize menu items under their respective food categories. |
| AC-VM-004 | The system shall display only published menu items to customers. |
| AC-VM-005 | The system shall display the current selling price for every visible menu item. |
| AC-VM-006 | The system shall clearly indicate the availability status of each menu item. |
| AC-VM-007 | The system shall display food type information (e.g., Vegetarian, Non-Vegetarian, Vegan, Egg) whenever available. |
| AC-VM-008 | The system shall display menu item images and short descriptions when they are available. |
| AC-VM-009 | The customer shall be able to select any visible menu item to view its detailed information. |
| AC-VM-010 | The system shall prevent unpublished, deleted, inactive, or unauthorized menu items from being displayed. |
| AC-VM-011 | The system shall display an appropriate message when no published menu is available for the selected restaurant. |
| AC-VM-012 | The system shall maintain data consistency by displaying the latest approved menu information available within the platform. |

### 3.3.2 View Food Categories

#### 3.3.2.1 Description

The View Food Categories functionality enables customers to browse the various food categories available within the selected restaurant's menu. Food categories provide a structured organization of menu items, allowing customers to quickly locate the type of food they wish to order.

The system shall retrieve and display all active food categories associated with the restaurant's latest published menu. Each category shall represent a logical grouping of menu items, such as Starters, Soups, Salads, Main Course, Rice, Noodles, Pizza, Burgers, Sandwiches, Desserts, Beverages, Breakfast, Lunch, Dinner, or any custom category defined by the restaurant.

The displayed food categories shall help customers navigate the restaurant menu efficiently without manually browsing every available menu item. Selecting a food category shall allow the customer to view the menu items belonging to that specific category.

The View Food Categories functionality shall ensure that customers always view the latest approved category information while preventing access to unpublished, deleted, disabled, or empty categories in accordance with the restaurant's business configuration.

#### 3.3.2.2 Actors

##### Primary Actor

- Customer

##### Supporting Actors

- Restaurant Service
- Menu Service
- Category Service
- Authentication Service (Optional, for personalized experiences)

#### 3.3.2.3 Preconditions

The following preconditions shall be satisfied before the customer can view the food categories of a restaurant:

1. The restaurant shall exist in the system.

2. The restaurant shall be approved and active.

3. The restaurant shall have at least one published menu.

4. The published menu shall contain one or more active food categories.

5. The customer shall have selected a restaurant from the search results, recommendations, favorites, order history, or any other valid navigation flow.

6. The system shall be able to communicate successfully with the Category Service.

7. The customer shall have network connectivity to retrieve the latest category information.

8. The system shall verify that the requested restaurant has not been permanently removed from the platform.

9. Category data shall be available for retrieval.

10. Customer authentication shall not be mandatory for viewing food categories unless restricted by business policies.

#### 3.3.2.4 Trigger

The View Food Categories functionality shall be initiated when the customer requests to view the food categories of a selected restaurant.

The functionality may be triggered through any of the following actions:

1. Selecting a restaurant from the restaurant listing.

2. Selecting a restaurant from the search results.

3. Selecting a restaurant from personalized recommendations.

4. Selecting a restaurant from the customer's favorite restaurants.

5. Selecting a restaurant from recent orders or order history.

6. Opening a restaurant through a shared restaurant link or promotional campaign.

Upon receiving the request, the system shall validate the selected restaurant and retrieve the active food categories associated with its latest published menu.

#### 3.3.2.5 Input Fields

| Field Name | Data Type | Mandatory | Description |
|------------|-----------|-----------|-------------|
| Restaurant ID | UUID / Integer | Yes | Unique identifier of the restaurant whose food categories are requested. |
| Customer ID | UUID / Integer | No | Unique identifier of the authenticated customer. Used for personalized category visibility where applicable. |
| Location | Latitude & Longitude / Address | No | Customer's delivery location used to determine serviceability and category availability, where applicable. |
| Language Preference | String | No | Preferred language in which the food category names should be displayed, if multilingual support is available. |

#### 3.3.2.6 Business Rules

The following business rules shall govern the View Food Categories functionality:

1. The system shall display only the active food categories associated with the latest published menu of the selected restaurant.

2. The system shall display food categories only for restaurants that are approved and currently active on the platform.

3. The system shall display food categories in the sequence configured by the restaurant.

4. Food categories that have been unpublished, deleted, disabled, or archived shall not be displayed to customers.

5. The system shall display only food categories that contain at least one visible menu item unless otherwise configured by the restaurant.

6. The system shall ensure that each displayed food category is associated with the selected restaurant only.

7. The system shall display the latest approved category information available within the platform.

8. The system shall display category names in the customer's preferred language where multilingual support is available.

9. The system shall ensure that customers can access the menu items belonging to a selected food category.

10. Viewing food categories shall not require customer authentication unless restricted by applicable business policies.

11. The system shall record category view activity for analytics, reporting, and recommendation purposes in accordance with applicable privacy policies.

12. The system shall ensure that only customers with appropriate access permissions can view food categories that are restricted to specific customer groups or promotional campaigns, where applicable.

#### 3.3.2.7 Validations

The system shall perform the following validations before displaying the food categories:

1. The system shall validate that the Restaurant ID is provided.

2. The system shall validate that the specified restaurant exists within the platform.

3. The system shall validate that the restaurant is approved and currently active.

4. The system shall validate that the restaurant is currently accepting customer requests, where applicable.

5. The system shall validate that a published menu exists for the selected restaurant.

6. The system shall validate that the published menu contains one or more active food categories.

7. The system shall validate that the food categories have not been deleted, archived, unpublished, or disabled.

8. The system shall validate that the customer is authorized to access restricted food categories, where applicable.

9. The system shall validate that category data is successfully retrieved from the Category Service.

10. The system shall validate that each food category belongs to the selected restaurant.

11. The system shall validate the customer's delivery location against the restaurant's service area, where location-based category visibility is applicable.

12. The system shall validate that all mandatory category information required for customer viewing is available before displaying the food categories.

#### 3.3.2.8 Main Flow

1. The customer selects a restaurant from the restaurant listing, search results, recommendations, favorites, order history, or any other valid navigation source.

2. The customer requests to view the food categories of the selected restaurant.

3. The system validates the restaurant and verifies that it is active, approved, and eligible to accept customer requests.

4. The system retrieves the latest published menu associated with the selected restaurant.

5. The system retrieves all active food categories associated with the published menu.

6. The system validates the visibility and accessibility of each food category before displaying it to the customer.

7. The system arranges the food categories according to the display sequence configured by the restaurant.

8. The system displays the available food categories to the customer.

9. The customer selects a food category of interest.

10. The system retrieves and displays the menu items associated with the selected food category.

11. The system records the category view activity for analytics and reporting purposes, where applicable.

12. The use case ends successfully after the selected food category and its associated menu items are displayed to the customer.

#### 3.3.2.9 Alternate Flows

##### AF-1: Restaurant Does Not Exist

1. The customer requests to view the food categories of a restaurant.
2. The system determines that the specified restaurant does not exist.
3. The system displays an appropriate error message indicating that the restaurant could not be found.
4. The use case ends.

---

##### AF-2: Restaurant Is Inactive or Not Approved

1. The customer requests to view the food categories.
2. The system determines that the restaurant is inactive, suspended, or not approved.
3. The system denies access to the food categories.
4. The system informs the customer that the restaurant is currently unavailable.
5. The use case ends.

---

##### AF-3: No Active Food Categories Available

1. The customer requests to view the food categories.
2. The system determines that the restaurant has no active food categories in its published menu.
3. The system informs the customer that no food categories are currently available.
4. The use case ends.

---

##### AF-4: Restaurant Is Outside the Service Area

1. The customer requests to view the food categories.
2. The system determines that the restaurant does not serve the customer's delivery location, where serviceability validation is applicable.
3. The system informs the customer that delivery is unavailable for the selected location.
4. The system may allow the customer to change the delivery location.
5. The use case continues after a valid delivery location is selected.

---

##### AF-5: Category Service Is Unavailable

1. The customer requests to view the food categories.
2. The system is unable to retrieve category information due to a temporary service failure.
3. The system displays an appropriate error message.
4. The system may allow the customer to retry the request.
5. The use case ends.

---

##### AF-6: Customer Is Not Authorized to View Food Categories

1. The customer requests to view restricted food categories.
2. The system determines that the customer does not satisfy the required access conditions.
3. The system denies access to the food categories.
4. The system displays an appropriate authorization message.
5. The use case ends.

#### 3.3.2.10 Postconditions

Upon completion of the View Food Categories functionality, one of the following postconditions shall apply:

##### Successful Completion

1. The active food categories associated with the selected restaurant's latest published menu shall be displayed to the customer.

2. The customer shall be able to browse the available food categories.

3. The customer shall be able to select a food category to view its associated menu items.

4. The system shall record the category view activity for analytics, reporting, and recommendation purposes, where applicable.

5. The system shall maintain the customer's current browsing session for subsequent menu navigation and ordering operations.

##### Unsuccessful Completion

1. The food categories shall not be displayed.

2. The system shall notify the customer of the reason the request could not be completed.

3. No changes shall be made to the restaurant's menu or category data.

4. The system shall maintain data integrity and prevent the display of incomplete, unpublished, or unauthorized category information.

#### 3.3.2.11 Success Response

Upon successful completion of the View Food Categories functionality, the system shall:

1. Display all active food categories associated with the selected restaurant's latest published menu.

2. Display the food categories in the sequence configured by the restaurant.

3. Display only categories that are available for customer browsing in accordance with the restaurant's business configuration.

4. Display the category name for each available food category.

5. Display the category image or icon, where available.

6. Allow the customer to select any displayed food category.

7. Display the menu items associated with the selected food category upon customer selection.

8. Present only the latest approved and published category information available within the platform.

9. Provide a consistent and responsive category browsing experience throughout the customer's session.

#### 3.3.2.12 Failure Response

If the View Food Categories functionality cannot be completed successfully, the system shall:

1. Inform the customer that the food categories could not be displayed.

2. Display an appropriate and user-friendly message describing the reason for the failure, where applicable.

3. Prevent the display of incomplete, unpublished, disabled, or unauthorized food category information.

4. Allow the customer to retry the request if the failure is temporary.

5. Allow the customer to return to the restaurant menu or continue browsing other available restaurants.

6. Record the failure event for system monitoring, diagnostics, and auditing purposes, where applicable.

7. Ensure that no category or menu data is modified as a result of the failed request.

8. Maintain the customer's current session and application state unless termination is required due to security or system policies.

#### 3.3.2.13 Acceptance Criteria

The View Food Categories functionality shall be considered successfully implemented when all the following conditions are satisfied:

| AC ID | Acceptance Criteria |
|-------|----------------------|
| AC-VFC-001 | The customer shall be able to view all active food categories associated with the selected restaurant's latest published menu. |
| AC-VFC-002 | The system shall display only food categories belonging to approved and active restaurants. |
| AC-VFC-003 | The system shall display food categories in the sequence configured by the restaurant. |
| AC-VFC-004 | The system shall display only active and published food categories. |
| AC-VFC-005 | The system shall prevent deleted, archived, disabled, or unpublished food categories from being displayed. |
| AC-VFC-006 | The system shall display the category name for each visible food category. |
| AC-VFC-007 | The system shall display the category image or icon where available. |
| AC-VFC-008 | The customer shall be able to select any displayed food category. |
| AC-VFC-009 | The system shall display the menu items associated with the selected food category. |
| AC-VFC-010 | The system shall display an appropriate message when no active food categories are available for the selected restaurant. |
| AC-VFC-011 | The system shall display only the latest approved category information available within the platform. |
| AC-VFC-012 | The system shall provide a consistent and responsive category browsing experience throughout the customer session. |

### 3.3.3 View Food Item Details

#### 3.3.3.1 Description

The View Food Item Details functionality enables customers to access comprehensive information about a selected menu item before making a purchase decision. After selecting a food item from the restaurant menu or a food category, the customer shall be able to view detailed information describing the item, its pricing, availability, ingredients, nutritional information, allergen information, available customizations, preparation details, and other relevant attributes.

The system shall retrieve the latest approved information associated with the selected menu item and present it in a clear, accurate, and user-friendly manner. The displayed information shall help customers understand the characteristics of the food item and make informed purchasing decisions based on their dietary preferences, health requirements, and customization needs.

The View Food Item Details functionality shall ensure that customers always view the latest published information for the selected menu item while preventing access to unpublished, deleted, disabled, or unauthorized menu items. Where applicable, the system shall also provide access to related information such as available variants, add-on options, preparation time, customer ratings, and applicable dietary indicators.

#### 3.3.3.2 Actors

##### Primary Actor

- Customer

##### Supporting Actors

- Restaurant Service
- Menu Service
- Item Service
- Inventory Service
- Pricing Service
- Customization Service
- Media Service
- Authentication Service (Optional, for personalized experiences)

#### 3.3.3.3 Preconditions

The following preconditions shall be satisfied before the customer can view the details of a food item:

1. The restaurant shall exist in the system.

2. The restaurant shall be approved and active.

3. The restaurant shall have at least one published menu.

4. The selected food item shall exist within the restaurant's published menu.

5. The selected food item shall be active and available for customer viewing.

6. The customer shall have selected a food item from the restaurant menu, food categories, search results, recommendations, favorites, or any other valid navigation flow.

7. The system shall be able to communicate successfully with the Item Service.

8. The customer shall have network connectivity to retrieve the latest food item information.

9. The system shall verify that the selected food item has not been permanently removed from the platform.

10. Customer authentication shall not be mandatory for viewing food item details unless restricted by applicable business policies.

#### 3.3.3.4 Trigger

The View Food Item Details functionality shall be initiated when the customer selects a food item from the restaurant menu or any valid food item listing.

The functionality may be triggered through any of the following actions:

1. Selecting a food item from the restaurant menu.

2. Selecting a food item from a food category.

3. Selecting a food item from the search results.

4. Selecting a food item from personalized recommendations.

5. Selecting a food item from the customer's favorite items.

6. Selecting a food item from recent orders or order history.

7. Opening a food item through a shared link, promotional campaign, or featured collection.

Upon receiving the request, the system shall validate the selected food item and retrieve its latest approved details for customer viewing.

#### 3.3.3.5 Input Fields

| Field Name | Data Type | Mandatory | Description |
|------------|-----------|-----------|-------------|
| Restaurant ID | UUID / Integer | Yes | Unique identifier of the restaurant associated with the selected food item. |
| Food Item ID | UUID / Integer | Yes | Unique identifier of the food item whose details are requested. |
| Customer ID | UUID / Integer | No | Unique identifier of the authenticated customer. Used for personalized information such as favorite status, recommendations, or customer-specific pricing where applicable. |
| Location | Latitude & Longitude / Address | No | Customer's delivery location used to determine item availability and serviceability, where applicable. |
| Language Preference | String | No | Preferred language in which the food item details should be displayed, if multilingual support is available. |

#### 3.3.3.6 Business Rules

The following business rules shall govern the View Food Item Details functionality:

1. The system shall display details only for food items that belong to the latest published menu of the selected restaurant.

2. The system shall display food item details only for restaurants that are approved and currently active on the platform.

3. The system shall display only food items that are active and available for customer viewing.

4. Food items that have been unpublished, deleted, archived, or disabled shall not be displayed to customers.

5. The system shall display the latest approved information associated with the selected food item.

6. The system shall display the current selling price configured for the selected food item.

7. The system shall display the food type classification (e.g., Vegetarian, Non-Vegetarian, Vegan, Egg) where applicable.

8. The system shall display the estimated preparation time for the selected food item, where available.

9. The system shall display the food item's short description, ingredients, nutritional information, allergen information, and available customization options where such information has been configured.

10. The system shall display all available variants, add-ons, toppings, and customization options associated with the selected food item, where applicable.

11. The system shall clearly indicate the current availability status of the selected food item.

12. The system shall display food item images only when valid media assets are available.

13. The system shall ensure that all displayed information corresponds to the selected food item and the selected restaurant.

14. Viewing food item details shall not require customer authentication unless restricted by applicable business policies.

15. The system shall record food item view activity for analytics, reporting, and recommendation purposes in accordance with applicable privacy policies.

16. The system shall ensure that only customers with appropriate access permissions can view restricted food items or promotional menu items, where applicable.

#### 3.3.3.7 Validations

The system shall perform the following validations before displaying the food item details:

1. The system shall validate that the Restaurant ID is provided.

2. The system shall validate that the Food Item ID is provided.

3. The system shall validate that the specified restaurant exists within the platform.

4. The system shall validate that the selected food item exists within the restaurant's latest published menu.

5. The system shall validate that the restaurant is approved and currently active.

6. The system shall validate that the selected food item is active and available for customer viewing.

7. The system shall validate that the selected food item has not been unpublished, deleted, archived, or disabled.

8. The system shall validate that the customer is authorized to access the selected food item if it is restricted by business policies or promotional conditions.

9. The system shall validate that the food item details are successfully retrieved from the Item Service.

10. The system shall validate that the displayed pricing information corresponds to the latest approved selling price of the selected food item.

11. The system shall validate the availability status of the selected food item before presenting it to the customer.

12. The system shall validate the customer's delivery location against the restaurant's service area, where location-based item visibility is applicable.

13. The system shall validate that all mandatory food item information required for customer viewing is available before displaying the food item details.

#### 3.3.3.8 Main Flow

1. The customer selects a food item from the restaurant menu, food category, search results, recommendations, favorites, order history, or any other valid navigation source.

2. The system receives the request to view the selected food item's details.

3. The system validates the restaurant and verifies that it is active, approved, and eligible to serve customer requests.

4. The system validates that the selected food item belongs to the restaurant's latest published menu.

5. The system retrieves the latest approved details associated with the selected food item.

6. The system retrieves the current pricing, availability status, food type, description, ingredients, nutritional information, allergen information, available variants, customization options, and associated media, where applicable.

7. The system validates the visibility and accessibility of the retrieved food item information before presenting it to the customer.

8. The system displays the complete food item details to the customer.

9. The customer reviews the displayed food item information.

10. The customer may proceed to customize the food item, add it to favorites, or add it to the shopping cart, where applicable.

11. The system records the food item view activity for analytics, reporting, and recommendation purposes, where applicable.

12. The use case ends successfully after the food item details are displayed to the customer.

#### 3.3.3.9 Alternate Flows

##### AF-1: Restaurant Does Not Exist

1. The customer requests to view the details of a food item.
2. The system determines that the specified restaurant does not exist.
3. The system displays an appropriate error message indicating that the restaurant could not be found.
4. The use case ends.

---

##### AF-2: Food Item Does Not Exist

1. The customer requests to view the details of a food item.
2. The system determines that the specified food item does not exist within the selected restaurant's published menu.
3. The system displays an appropriate error message indicating that the food item could not be found.
4. The use case ends.

---

##### AF-3: Food Item Is Unavailable

1. The customer requests to view the details of a food item.
2. The system determines that the food item is unavailable, disabled, unpublished, or archived.
3. The system informs the customer that the food item is currently unavailable.
4. The use case ends.

---

##### AF-4: Restaurant Is Outside the Service Area

1. The customer requests to view the details of a food item.
2. The system determines that the restaurant does not serve the customer's delivery location, where serviceability validation is applicable.
3. The system informs the customer that delivery is unavailable for the selected location.
4. The system may allow the customer to change the delivery location.
5. The use case continues after a valid delivery location is selected.

---

##### AF-5: Item Service Is Unavailable

1. The customer requests to view the details of a food item.
2. The system is unable to retrieve the food item details due to a temporary service failure.
3. The system displays an appropriate error message.
4. The system may allow the customer to retry the request.
5. The use case ends.

---

##### AF-6: Customer Is Not Authorized to View the Food Item

1. The customer requests to view a restricted food item.
2. The system determines that the customer does not satisfy the required access conditions.
3. The system denies access to the food item details.
4. The system displays an appropriate authorization message.
5. The use case ends.

#### 3.3.3.10 Postconditions

Upon completion of the View Food Item Details functionality, one of the following postconditions shall apply:

##### Successful Completion

1. The complete details of the selected food item shall be displayed to the customer.

2. The customer shall be able to review the food item's pricing, availability, description, ingredients, nutritional information, allergen information, variants, and available customization options, where applicable.

3. The customer shall be able to proceed to customize the food item, add it to favorites, or add it to the shopping cart, where applicable.

4. The system shall record the food item view activity for analytics, reporting, and recommendation purposes, where applicable.

5. The system shall maintain the customer's current browsing session for subsequent menu navigation and ordering operations.

##### Unsuccessful Completion

1. The food item details shall not be displayed.

2. The system shall notify the customer of the reason the request could not be completed.

3. No changes shall be made to the food item, menu, or restaurant data.

4. The system shall maintain data integrity and prevent the display of incomplete, unpublished, deleted, disabled, or unauthorized food item information.

#### 3.3.3.11 Success Response

Upon successful completion of the View Food Item Details functionality, the system shall:

1. Display the latest approved details of the selected food item.

2. Display the food item's name, price, availability status, and food type classification.

3. Display the food item's description, ingredients, nutritional information, and allergen information, where available.

4. Display the available variants, add-ons, toppings, and customization options associated with the selected food item, where applicable.

5. Display the estimated preparation time for the selected food item, where available.

6. Display the food item's images and other associated media, where available.

7. Allow the customer to proceed with supported actions such as customizing the food item, adding it to favorites, or adding it to the shopping cart, where applicable.

8. Present only the latest approved and published food item information available within the platform.

9. Provide a consistent, accurate, and responsive food item viewing experience throughout the customer's session.

#### 3.3.3.12 Failure Response

If the View Food Item Details functionality cannot be completed successfully, the system shall:

1. Inform the customer that the food item details could not be displayed.

2. Display an appropriate and user-friendly message describing the reason for the failure, where applicable.

3. Prevent the display of incomplete, unpublished, deleted, disabled, or unauthorized food item information.

4. Allow the customer to retry the request if the failure is temporary.

5. Allow the customer to return to the restaurant menu, food category, or continue browsing other available food items.

6. Record the failure event for system monitoring, diagnostics, and auditing purposes, where applicable.

7. Ensure that no food item, menu, or restaurant data is modified as a result of the failed request.

8. Maintain the customer's current session and application state unless termination is required due to security or system policies.

#### 3.3.3.12 Failure Response

If the View Food Item Details functionality cannot be completed successfully, the system shall:

1. Inform the customer that the food item details could not be displayed.

2. Display an appropriate and user-friendly message describing the reason for the failure, where applicable.

3. Prevent the display of incomplete, unpublished, deleted, disabled, or unauthorized food item information.

4. Allow the customer to retry the request if the failure is temporary.

5. Allow the customer to return to the restaurant menu, food category, or continue browsing other available food items.

6. Record the failure event for system monitoring, diagnostics, and auditing purposes, where applicable.

7. Ensure that no food item, menu, or restaurant data is modified as a result of the failed request.

8. Maintain the customer's current session and application state unless termination is required due to security or system policies.

#### 3.3.3.13 Acceptance Criteria

The View Food Item Details functionality shall be considered successfully implemented when all the following conditions are satisfied:

| AC ID | Acceptance Criteria |
|-------|----------------------|
| AC-VFID-001 | The customer shall be able to view the latest approved details of the selected food item. |
| AC-VFID-002 | The system shall display food item details only for active and approved restaurants. |
| AC-VFID-003 | The system shall display only active and published food items. |
| AC-VFID-004 | The system shall display the current selling price of the selected food item. |
| AC-VFID-005 | The system shall display the food type classification and availability status of the selected food item, where applicable. |
| AC-VFID-006 | The system shall display the food item's description, ingredients, nutritional information, and allergen information when configured. |
| AC-VFID-007 | The system shall display all available variants, add-ons, toppings, and customization options associated with the selected food item, where applicable. |
| AC-VFID-008 | The system shall display the food item's images and associated media when available. |
| AC-VFID-009 | The customer shall be able to proceed with supported actions such as customizing the food item, adding it to favorites, or adding it to the shopping cart. |
| AC-VFID-010 | The system shall prevent unpublished, deleted, archived, disabled, or unauthorized food items from being displayed. |
| AC-VFID-011 | The system shall display an appropriate message when the requested food item is unavailable or cannot be accessed. |
| AC-VFID-012 | The system shall display only the latest approved food item information available within the platform. |
| AC-VFID-013 | The system shall provide a consistent, accurate, and responsive food item viewing experience throughout the customer's session. |

### 3.3.4 Search Menu Items

#### 3.3.4.1 Description

The Search Menu Items functionality enables customers to search for specific food items within a restaurant's menu using relevant keywords or phrases. The functionality helps customers quickly locate desired food items without manually browsing through the entire menu or multiple food categories.

The system shall search the latest published menu of the selected restaurant and retrieve food items whose names, descriptions, or other searchable attributes match the customer's search criteria. The search results shall include only active, published, and customer-visible food items that satisfy the search conditions.

The Search Menu Items functionality shall provide accurate and responsive search results while preventing unpublished, deleted, disabled, or unauthorized food items from appearing in the search results. Where applicable, the system may support partial keyword matching, case-insensitive searching, and multilingual search capabilities based on the platform configuration.

#### 3.3.4.2 Actors

##### Primary Actor

- Customer

##### Supporting Actors

- Restaurant Service
- Menu Service
- Search Service
- Item Service
- Authentication Service (Optional, for personalized search experiences)

#### 3.3.4.3 Preconditions

The following preconditions shall be satisfied before the customer can search for menu items:

1. The restaurant shall exist in the system.

2. The restaurant shall be approved and active.

3. The restaurant shall have at least one published menu.

4. The published menu shall contain one or more searchable food items.

5. The customer shall have selected a restaurant before initiating the search.

6. The system shall be able to communicate successfully with the Search Service.

7. The customer shall have network connectivity to perform the search operation.

8. The system shall verify that the selected restaurant has not been permanently removed from the platform.

9. Searchable menu data shall be available for retrieval.

10. Customer authentication shall not be mandatory for searching menu items unless restricted by applicable business policies.

#### 3.3.4.4 Trigger

The Search Menu Items functionality shall be initiated when the customer enters a search keyword or phrase to find food items within the selected restaurant's menu.

The functionality may be triggered through any of the following actions:

1. Entering a keyword in the restaurant menu search field.

2. Selecting a suggested search keyword or recent search.

3. Selecting a popular or trending search suggestion.

4. Modifying an existing search query.

5. Clearing and entering a new search keyword.

Upon receiving the search request, the system shall validate the search input and retrieve the matching food items from the selected restaurant's latest published menu.

#### 3.3.4.5 Input Fields

| Field Name | Data Type | Mandatory | Description |
|------------|-----------|-----------|-------------|
| Restaurant ID | UUID / Integer | Yes | Unique identifier of the restaurant within which the search is performed. |
| Search Keyword | String | Yes | Keyword or phrase entered by the customer to search for menu items. |
| Customer ID | UUID / Integer | No | Unique identifier of the authenticated customer. Used for personalized search results where applicable. |
| Language Preference | String | No | Preferred language used for searching and displaying menu items, where multilingual support is available. |
| Location | Latitude & Longitude / Address | No | Customer's delivery location used to determine item visibility and serviceability, where applicable. |

#### 3.3.4.6 Business Rules

The following business rules shall govern the Search Menu Items functionality:

1. The system shall search only within the latest published menu of the selected restaurant.

2. The system shall return only food items that are active, published, and available for customer viewing.

3. The system shall search food items based on the customer's search keyword or phrase.

4. The system shall support partial keyword matching where configured by the platform.

5. The system shall perform case-insensitive searches unless otherwise restricted by business policies.

6. The system shall search across applicable food item attributes, including the food item name, short description, category name, and searchable keywords, where configured.

7. The system shall exclude unpublished, deleted, archived, disabled, or unauthorized food items from the search results.

8. The system shall display search results only for the selected restaurant and shall not include food items from other restaurants.

9. The system shall display the latest approved information for each matching food item.

10. The system shall indicate the current availability status of each matching food item.

11. The system shall display the current selling price of each matching food item.

12. The system shall display matching food items in accordance with the platform's search relevance and ranking policies.

13. The system shall return an appropriate response when no matching food items are found.

14. The system shall record customer search activity for analytics, reporting, recommendation, and search optimization purposes in accordance with applicable privacy policies.

15. Searching menu items shall not require customer authentication unless restricted by applicable business policies.

#### 3.3.4.7 Validations

The system shall perform the following validations before processing the menu item search request:

1. The system shall validate that the Restaurant ID is provided.

2. The system shall validate that the Search Keyword is provided.

3. The system shall validate that the specified restaurant exists within the platform.

4. The system shall validate that the restaurant is approved and currently active.

5. The system shall validate that the selected restaurant has a published menu available for searching.

6. The system shall validate that the Search Keyword satisfies the platform's input validation rules, including supported character sets and maximum length.

7. The system shall validate that the customer is authorized to search restricted menu items, where applicable.

8. The system shall validate that the search request is successfully processed by the Search Service.

9. The system shall validate that only food items belonging to the selected restaurant are included in the search results.

10. The system shall validate that each matching food item is active, published, and visible to the customer.

11. The system shall validate the customer's delivery location against the restaurant's service area, where location-based menu visibility is applicable.

12. The system shall validate that the search results contain only the latest approved food item information before displaying them to the customer.

#### 3.3.4.8 Main Flow

1. The customer navigates to the selected restaurant's menu.

2. The customer enters a search keyword or phrase in the menu search field.

3. The system receives the search request.

4. The system validates the search request and verifies that the selected restaurant is active and has a published menu.

5. The system searches the restaurant's latest published menu for food items matching the customer's search criteria.

6. The system filters the search results to include only active, published, and customer-visible food items.

7. The system ranks the matching food items according to the platform's search relevance rules.

8. The system retrieves the latest approved information for each matching food item.

9. The system displays the matching food items to the customer.

10. The customer reviews the search results.

11. The customer may select a food item to view its detailed information.

12. The system records the search activity for analytics, reporting, recommendation, and search optimization purposes, where applicable.

13. The use case ends successfully after the matching food items are displayed to the customer.

#### 3.3.4.9 Alternate Flows

##### AF-1: Restaurant Does Not Exist

1. The customer initiates a menu item search.
2. The system determines that the specified restaurant does not exist.
3. The system displays an appropriate error message indicating that the restaurant could not be found.
4. The use case ends.

---

##### AF-2: Search Keyword Is Invalid

1. The customer submits an invalid or unsupported search keyword.
2. The system validates the search input and determines that it does not satisfy the platform's input validation rules.
3. The system informs the customer to provide a valid search keyword.
4. The customer may modify the search keyword and retry the search.
5. The use case continues after a valid search keyword is provided.

---

##### AF-3: No Matching Food Items Found

1. The customer searches for a menu item.
2. The system completes the search but does not find any matching food items.
3. The system informs the customer that no matching food items were found.
4. The system may display suggested or popular menu items, where applicable.
5. The use case ends.

---

##### AF-4: Restaurant Is Outside the Service Area

1. The customer searches for menu items.
2. The system determines that the restaurant does not serve the customer's delivery location, where serviceability validation is applicable.
3. The system informs the customer that delivery is unavailable for the selected location.
4. The system may allow the customer to change the delivery location.
5. The use case continues after a valid delivery location is selected.

---

##### AF-5: Search Service Is Unavailable

1. The customer initiates a menu item search.
2. The system is unable to process the search request due to a temporary Search Service failure.
3. The system displays an appropriate error message.
4. The system may allow the customer to retry the search.
5. The use case ends.

---

##### AF-6: Customer Is Not Authorized to Search Restricted Menu Items

1. The customer searches for menu items.
2. The system determines that the search request includes restricted menu items that require special access permissions.
3. The system excludes the restricted menu items from the search results or denies access in accordance with business policies.
4. The system displays an appropriate authorization message, where applicable.
5. The use case ends.

#### 3.3.4.10 Postconditions

Upon completion of the Search Menu Items functionality, one of the following postconditions shall apply:

##### Successful Completion

1. The matching food items shall be displayed to the customer.

2. The customer shall be able to review the search results.

3. The customer shall be able to select any matching food item to view its detailed information.

4. The system shall record the customer's search activity for analytics, reporting, recommendation, and search optimization purposes, where applicable.

5. The system shall maintain the customer's current search context and browsing session for subsequent menu navigation and ordering operations.

##### Unsuccessful Completion

1. The search results shall not be displayed.

2. The system shall notify the customer of the reason the search request could not be completed.

3. No changes shall be made to the restaurant's menu, food item, or search data.

4. The system shall maintain data integrity and prevent the display of unpublished, deleted, disabled, or unauthorized food items.

5. The customer's existing browsing session shall remain active unless termination is required due to security or system policies.

#### 3.3.4.11 Success Response

Upon successful completion of the Search Menu Items functionality, the system shall:

1. Display the food items that match the customer's search keyword or phrase.

2. Display only active, published, and customer-visible food items in the search results.

3. Display the current selling price and availability status of each matching food item.

4. Display the food item image, where available.

5. Display the food category associated with each matching food item, where applicable.

6. Display the latest approved information for each matching food item.

7. Allow the customer to select any displayed food item to view its detailed information.

8. Display the search results in accordance with the platform's search relevance and ranking policies.

9. Provide a consistent, accurate, and responsive search experience throughout the customer's session.

#### 3.3.4.12 Failure Response

If the Search Menu Items functionality cannot be completed successfully, the system shall:

1. Inform the customer that the search request could not be completed.

2. Display an appropriate and user-friendly message describing the reason for the failure, where applicable.

3. Display an appropriate message when no matching food items are found.

4. Prevent the display of unpublished, deleted, disabled, or unauthorized food items in the search results.

5. Allow the customer to modify the search keyword and perform a new search.

6. Allow the customer to continue browsing the restaurant menu if the search request is unsuccessful.

7. Record the search failure event for system monitoring, diagnostics, auditing, and search performance analysis, where applicable.

8. Ensure that no restaurant, menu, food item, or search data is modified as a result of the failed search request.

9. Maintain the customer's current session and application state unless termination is required due to security or system policies.

#### 3.3.4.13 Acceptance Criteria

The Search Menu Items functionality shall be considered successfully implemented when all the following conditions are satisfied:

| AC ID | Acceptance Criteria |
|-------|----------------------|
| AC-SMI-001 | The customer shall be able to search for menu items using a valid keyword or phrase within the selected restaurant. |
| AC-SMI-002 | The system shall search only within the latest published menu of the selected restaurant. |
| AC-SMI-003 | The system shall return only active, published, and customer-visible food items in the search results. |
| AC-SMI-004 | The system shall support partial keyword matching where configured by the platform. |
| AC-SMI-005 | The system shall perform case-insensitive searches unless otherwise restricted by business policies. |
| AC-SMI-006 | The system shall display the latest approved information for each matching food item. |
| AC-SMI-007 | The system shall display the current selling price and availability status of each matching food item. |
| AC-SMI-008 | The system shall display the food item image and associated food category, where available. |
| AC-SMI-009 | The customer shall be able to select any matching food item to view its detailed information. |
| AC-SMI-010 | The system shall display an appropriate message when no matching food items are found. |
| AC-SMI-011 | The system shall exclude unpublished, deleted, disabled, archived, or unauthorized food items from the search results. |
| AC-SMI-012 | The system shall display search results in accordance with the platform's search relevance and ranking policies. |
| AC-SMI-013 | The system shall provide a consistent, accurate, and responsive search experience throughout the customer's session. |

### 3.3.5 Filter Menu Items

#### 3.3.5.1 Description

The Filter Menu Items functionality enables customers to refine the displayed menu items by applying one or more predefined filter criteria. The system shall display only the food items that satisfy the selected filter options while ensuring that only active, published, and customer-visible menu items are returned. This functionality improves the customer's ability to quickly discover food items that match their preferences and ordering requirements.

#### 3.3.5.2 Actors

**Primary Actor**

- Customer

**Supporting Actors**

- Menu Service
- Restaurant Service
- Search and Filter Service
- Authentication and Authorization Service (where applicable)

#### 3.3.5.3 Preconditions

1. The customer shall have access to the QuickBite platform.

2. The selected restaurant shall exist and be available for customer access.

3. The restaurant shall have at least one published menu.

4. The published menu shall contain active and customer-visible food items.

5. The available filter options shall be configured by the platform.

6. The customer shall have opened the restaurant menu before applying filters.

#### 3.3.5.4 Trigger

The use case begins when the customer selects one or more filter options while viewing the restaurant menu.

#### 3.3.5.5 Input Fields

| Field | Description | Mandatory |
|-------|-------------|-----------|
| Restaurant ID | Unique identifier of the selected restaurant | Yes |
| Filter Criteria | One or more selected filter options | Yes |
| Food Category | Selected food category filter, where applicable | No |
| Food Type | Vegetarian, Non-Vegetarian, Vegan, Egg, etc. | No |
| Price Range | Minimum and/or maximum price range | No |
| Availability Status | Available or Currently Unavailable | No |
| Sort Preference | Optional sorting preference after filtering | No |

#### 3.3.5.6 Business Rules

1. The system shall apply filters only to the latest published menu of the selected restaurant.

2. The system shall display only active, published, and customer-visible food items after applying the selected filters.

3. The customer may apply one or more filter criteria simultaneously.

4. The system shall return only the food items that satisfy all selected filter criteria.

5. The system shall support filtering based on platform-configured criteria, including food category, food type, price range, availability status, and other supported attributes.

6. The system shall ignore filter criteria that are not supported or configured by the platform.

7. The system shall update the displayed menu items immediately after the selected filters are applied.

8. The customer may modify, add, or remove filter criteria at any time while viewing the restaurant menu.

9. The customer may clear all applied filters and return to the complete restaurant menu.

10. The system shall not display unpublished, deleted, disabled, archived, or unauthorized food items regardless of the selected filter criteria.

11. The system shall preserve the applied filter criteria during the customer's current browsing session unless the customer clears the filters or leaves the restaurant menu.

12. The system shall record filter usage for analytics, reporting, recommendation, and product improvement purposes, where applicable.

#### 3.3.5.7 Validations

1. The system shall validate that the selected restaurant exists before applying any filter criteria.

2. The system shall validate that the restaurant has a published menu available for customer access.

3. The system shall validate that each selected filter criterion is supported by the platform.

4. The system shall validate that the selected food category exists within the restaurant menu, where applicable.

5. The system shall validate that the selected food type is a supported classification.

6. The system shall validate that the specified price range contains valid numeric values.

7. The system shall validate that the minimum price is less than or equal to the maximum price, where both values are provided.

8. The system shall validate that the selected availability status is supported by the platform.

9. The system shall ignore duplicate filter selections where applicable.

10. The system shall validate that the customer is authorized to view the requested menu items, where access restrictions apply.

11. The system shall ensure that unpublished, deleted, disabled, archived, or unauthorized food items are excluded from the filtered results.

12. The system shall validate all filter inputs before processing the filter request.

#### 3.3.5.8 Main Flow

1. The customer opens the menu of the selected restaurant.

2. The customer selects one or more filter criteria.

3. The system receives the filter request.

4. The system validates the selected filter criteria.

5. The system retrieves the latest published menu for the selected restaurant.

6. The system filters the menu items based on the selected criteria.

7. The system excludes unpublished, deleted, disabled, archived, or unauthorized food items from the filtered results.

8. The system retrieves the latest approved information for all matching food items.

9. The system displays the filtered menu items to the customer.

10. The customer reviews the filtered results.

11. The customer may modify, add, remove, or clear the applied filters.

12. The system refreshes the displayed menu items based on the updated filter criteria.

13. The system records filter usage for analytics and reporting purposes.

14. The use case ends successfully.

#### 3.3.5.9 Alternate Flows

##### AF-1: Restaurant Does Not Exist

1. The customer attempts to apply one or more filters.
2. The system determines that the selected restaurant does not exist.
3. The system displays an appropriate error message indicating that the restaurant could not be found.
4. The use case ends.

---

##### AF-2: Published Menu Is Not Available

1. The customer applies filter criteria.
2. The system determines that the restaurant does not have a published menu.
3. The system informs the customer that the menu is currently unavailable.
4. The use case ends.

---

##### AF-3: Invalid Filter Criteria

1. The customer selects one or more unsupported or invalid filter criteria.
2. The system validates the filter request and identifies the invalid criteria.
3. The system displays an appropriate validation message.
4. The customer may modify the filter selection and retry.
5. The use case continues after valid filter criteria are provided.

---

##### AF-4: No Matching Food Items Found

1. The customer applies valid filter criteria.
2. The system successfully processes the request but finds no food items matching all selected filters.
3. The system displays an appropriate message indicating that no matching food items were found.
4. The system may allow the customer to modify or clear the applied filters.
5. The use case ends.

---

##### AF-5: Customer Clears All Filters

1. The customer selects the option to clear all applied filters.
2. The system removes all active filter criteria.
3. The system retrieves the complete published menu for the selected restaurant.
4. The system displays all eligible menu items.
5. The use case continues.

---

##### AF-6: Filter Service Is Unavailable

1. The customer applies one or more filter criteria.
2. The system is unable to process the filter request due to a temporary Filter Service failure.
3. The system displays an appropriate error message.
4. The customer may retry the operation later.
5. The use case ends.

---

##### AF-7: Customer Is Not Authorized to View Certain Menu Items

1. The customer applies filter criteria.
2. The system determines that one or more matching food items are restricted based on authorization or business policies.
3. The system excludes the restricted food items from the filtered results.
4. The system displays only the food items the customer is authorized to view.
5. The use case ends.

#### 3.3.5.10 Postconditions

Upon completion of the Filter Menu Items functionality, one of the following postconditions shall apply:

##### Successful Completion

1. The filtered menu items shall be displayed to the customer based on the selected filter criteria.

2. Only active, published, and customer-visible food items that satisfy the selected filters shall be displayed.

3. The customer shall be able to review the filtered menu items.

4. The customer shall be able to modify, add, remove, or clear the applied filter criteria.

5. The system shall preserve the applied filter criteria during the customer's current browsing session unless the customer clears the filters or leaves the restaurant menu.

6. The system shall record the customer's filter activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

##### Unsuccessful Completion

1. The filtered menu items shall not be displayed.

2. The system shall notify the customer of the reason the filter request could not be completed.

3. No changes shall be made to the restaurant's menu, food item, or filter configuration.

4. The system shall maintain data integrity and prevent the display of unpublished, deleted, disabled, archived, or unauthorized food items.

5. The customer's existing browsing session shall remain active unless termination is required due to security or system policies.

#### 3.3.5.11 Success Response

Upon successful completion of the Filter Menu Items functionality, the system shall:

1. Display the food items that satisfy the selected filter criteria.

2. Display only active, published, and customer-visible food items in the filtered results.

3. Display the current selling price and availability status of each filtered food item.

4. Display the food item image, where available.

5. Display the food category and food type associated with each filtered food item, where applicable.

6. Display the latest approved information for each filtered food item.

7. Allow the customer to modify, add, remove, or clear the applied filter criteria.

8. Refresh the displayed menu items immediately after any change to the selected filter criteria.

9. Allow the customer to select any displayed food item to view its detailed information.

10. Provide a consistent, accurate, and responsive filtering experience throughout the customer's browsing session.

#### 3.3.5.12 Failure Response

If the Filter Menu Items functionality cannot be completed successfully, the system shall:

1. Inform the customer that the filter request could not be completed.

2. Display an appropriate and user-friendly message describing the reason for the failure, where applicable.

3. Display an appropriate message when no food items match the selected filter criteria.

4. Prevent the display of unpublished, deleted, disabled, archived, or unauthorized food items in the filtered results.

5. Allow the customer to modify, remove, or clear the selected filter criteria and retry the operation.

6. Allow the customer to continue browsing the complete restaurant menu if the filter request is unsuccessful.

7. Record the filter failure event for system monitoring, diagnostics, auditing, and analytics purposes, where applicable.

8. Ensure that no restaurant, menu, food item, or filter configuration data is modified as a result of the failed filter request.

9. Maintain the customer's current browsing session and application state unless termination is required due to security or system policies.

#### 3.3.5.13 Acceptance Criteria

The Filter Menu Items functionality shall be considered successfully implemented when all the following conditions are satisfied:

| AC ID | Acceptance Criteria |
|-------|----------------------|
| AC-FMI-001 | The customer shall be able to apply one or more filter criteria while viewing the restaurant menu. |
| AC-FMI-002 | The system shall apply filters only to the latest published menu of the selected restaurant. |
| AC-FMI-003 | The system shall display only active, published, and customer-visible food items that satisfy the selected filter criteria. |
| AC-FMI-004 | The system shall support the application of multiple filter criteria simultaneously. |
| AC-FMI-005 | The system shall return only the food items that satisfy all selected filter criteria. |
| AC-FMI-006 | The system shall support filtering based on platform-configured criteria such as food category, food type, price range, and availability status. |
| AC-FMI-007 | The customer shall be able to modify, add, remove, or clear the applied filter criteria at any time. |
| AC-FMI-008 | The system shall refresh the displayed menu items immediately after the filter criteria are updated. |
| AC-FMI-009 | The customer shall be able to select any displayed food item to view its detailed information. |
| AC-FMI-010 | The system shall display an appropriate message when no food items match the selected filter criteria. |
| AC-FMI-011 | The system shall exclude unpublished, deleted, disabled, archived, or unauthorized food items from the filtered results. |
| AC-FMI-012 | The system shall preserve the applied filter criteria during the customer's current browsing session unless the customer clears the filters or leaves the restaurant menu. |
| AC-FMI-013 | The system shall provide a consistent, accurate, and responsive filtering experience throughout the customer's session. |

### 3.3.6 Sort Menu Items

#### 3.3.6.1 Description

The Sort Menu Items functionality enables customers to arrange the displayed menu items according to one or more predefined sorting options. The system shall sort only the active, published, and customer-visible food items based on the selected sorting criterion while preserving the integrity of the restaurant's menu data. This functionality helps customers quickly locate menu items according to their preferences, such as price, popularity, customer rating, or other platform-supported sorting options.

#### 3.3.6.2 Actors

**Primary Actor**

- Customer

**Supporting Actors**

- Menu Service
- Restaurant Service
- Search and Sort Service
- Authentication and Authorization Service (where applicable)

#### 3.3.6.3 Preconditions

1. The customer shall have access to the QuickBite platform.

2. The selected restaurant shall exist and be available for customer access.

3. The restaurant shall have at least one published menu.

4. The published menu shall contain active and customer-visible food items.

5. The available sorting options shall be configured by the platform.

6. The customer shall have opened the restaurant menu before applying a sorting option.

#### 3.3.6.4 Trigger

The use case begins when the customer selects a sorting option while viewing the restaurant menu.

#### 3.3.6.5 Input Fields

| Field | Description | Mandatory |
|-------|-------------|-----------|
| Restaurant ID | Unique identifier of the selected restaurant | Yes |
| Sort Option | Selected sorting criterion | Yes |
| Sort Order | Ascending or Descending, where applicable | No |

#### 3.3.6.6 Business Rules

1. The system shall apply sorting only to the latest published menu of the selected restaurant.

2. The system shall display only active, published, and customer-visible food items after applying the selected sorting option.

3. The customer may select only one sorting option at a time.

4. The system shall support only platform-configured sorting options.

5. The system shall arrange the displayed food items according to the selected sorting criterion.

6. The system shall preserve any previously applied search keyword or filter criteria while applying the selected sorting option, where applicable.

7. The customer may change the selected sorting option at any time while viewing the restaurant menu.

8. The customer may remove the applied sorting option and return to the platform's default menu ordering.

9. The system shall not modify the restaurant's actual menu sequence or business data while performing the sorting operation.

10. The system shall not display unpublished, deleted, disabled, archived, or unauthorized food items regardless of the selected sorting option.

11. The system shall preserve the selected sorting option during the customer's current browsing session unless the customer changes the sorting option, resets the sorting preference, or leaves the restaurant menu.

12. The system shall record sorting activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

#### 3.3.6.7 Validations

1. The system shall validate that the selected restaurant exists before applying the sorting option.

2. The system shall validate that the restaurant has a published menu available for customer access.

3. The system shall validate that the selected sorting option is supported by the platform.

4. The system shall validate that the selected sorting order is applicable to the chosen sorting option, where applicable.

5. The system shall validate that the customer is authorized to view the requested menu items, where access restrictions apply.

6. The system shall ensure that unpublished, deleted, disabled, archived, or unauthorized food items are excluded from the sorted results.

7. The system shall validate that the menu contains eligible food items before performing the sorting operation.

8. The system shall ignore duplicate sorting requests if the currently selected sorting option is already applied.

9. The system shall validate all sorting inputs before processing the sorting request.

10. The system shall reject unsupported or invalid sorting parameters and display an appropriate validation message.

11. The system shall preserve any valid search keywords and filter criteria while validating the sorting request, where applicable.

12. The system shall ensure that sorting does not modify the underlying restaurant menu data or business records.

#### 3.3.6.8 Main Flow

1. The customer opens the menu of the selected restaurant.

2. The customer selects a sorting option.

3. The system receives the sorting request.

4. The system validates the selected sorting option.

5. The system retrieves the latest published menu for the selected restaurant.

6. The system preserves any existing search keywords and filter criteria, where applicable.

7. The system arranges the eligible food items according to the selected sorting option.

8. The system excludes unpublished, deleted, disabled, archived, or unauthorized food items from the sorted results.

9. The system retrieves the latest approved information for all displayed food items.

10. The system displays the sorted menu items to the customer.

11. The customer reviews the sorted menu items.

12. The customer may change or remove the selected sorting option.

13. The system refreshes the displayed menu items based on the updated sorting preference.

14. The system records sorting activity for analytics and reporting purposes.

15. The use case ends successfully.

#### 3.3.6.9 Alternate Flows

##### AF-1: Restaurant Does Not Exist

1. The customer attempts to apply a sorting option.
2. The system determines that the selected restaurant does not exist.
3. The system displays an appropriate error message indicating that the restaurant could not be found.
4. The use case ends.

---

##### AF-2: Published Menu Is Not Available

1. The customer selects a sorting option.
2. The system determines that the restaurant does not have a published menu.
3. The system informs the customer that the menu is currently unavailable.
4. The use case ends.

---

##### AF-3: Invalid Sorting Option

1. The customer selects an unsupported or invalid sorting option.
2. The system validates the sorting request and identifies the invalid sorting option.
3. The system displays an appropriate validation message.
4. The customer may select a valid sorting option and retry.
5. The use case continues after a valid sorting option is selected.

---

##### AF-4: No Eligible Food Items Available for Sorting

1. The customer applies a sorting option.
2. The system determines that there are no eligible food items available for sorting.
3. The system displays an appropriate message indicating that no food items are available.
4. The use case ends.

---

##### AF-5: Customer Resets Sorting Preference

1. The customer selects the option to reset or remove the applied sorting preference.
2. The system removes the current sorting option.
3. The system restores the platform's default menu ordering.
4. The system displays the menu items using the default ordering.
5. The use case continues.

---

##### AF-6: Sort Service Is Unavailable

1. The customer selects a sorting option.
2. The system is unable to process the sorting request due to a temporary Sort Service failure.
3. The system displays an appropriate error message.
4. The customer may retry the operation later.
5. The use case ends.

---

##### AF-7: Customer Is Not Authorized to View Certain Menu Items

1. The customer applies a sorting option.
2. The system determines that one or more menu items are restricted based on authorization or business policies.
3. The system excludes the restricted menu items from the sorted results.
4. The system displays only the menu items the customer is authorized to view.
5. The use case ends.

#### 3.3.6.10 Postconditions

Upon completion of the Sort Menu Items functionality, one of the following postconditions shall apply:

##### Successful Completion

1. The menu items shall be displayed according to the selected sorting option.

2. Only active, published, and customer-visible food items shall be included in the sorted results.

3. The customer shall be able to review the sorted menu items.

4. The customer shall be able to change, replace, or reset the applied sorting option.

5. Any previously applied search keywords and filter criteria shall remain preserved, where applicable.

6. The system shall record the customer's sorting activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

##### Unsuccessful Completion

1. The requested sorting operation shall not be applied.

2. The system shall notify the customer of the reason the sorting request could not be completed.

3. The previously displayed menu ordering shall remain unchanged.

4. No changes shall be made to the restaurant's menu, food item, or sorting configuration.

5. The system shall maintain data integrity and prevent the display of unpublished, deleted, disabled, archived, or unauthorized food items.

6. The customer's existing browsing session shall remain active unless termination is required due to security or system policies.

#### 3.3.6.11 Success Response

Upon successful completion of the Sort Menu Items functionality, the system shall:

1. Display the menu items arranged according to the selected sorting option.

2. Display only active, published, and customer-visible food items in the sorted results.

3. Display the current selling price and availability status of each displayed food item.

4. Display the food item image, where available.

5. Display the food category and food type associated with each displayed food item, where applicable.

6. Display the latest approved information for each displayed food item.

7. Preserve any previously applied search keywords and filter criteria while displaying the sorted results, where applicable.

8. Allow the customer to change, replace, or reset the selected sorting option.

9. Refresh the displayed menu items immediately after the sorting preference is updated.

10. Allow the customer to select any displayed food item to view its detailed information.

11. Provide a consistent, accurate, and responsive sorting experience throughout the customer's browsing session.

#### 3.3.6.12 Failure Response

If the Sort Menu Items functionality cannot be completed successfully, the system shall:

1. Inform the customer that the sorting request could not be completed.

2. Display an appropriate and user-friendly message describing the reason for the failure, where applicable.

3. Preserve the previously displayed menu ordering if the requested sorting operation fails.

4. Prevent the display of unpublished, deleted, disabled, archived, or unauthorized food items in the sorted results.

5. Allow the customer to select a different sorting option or retry the sorting operation.

6. Allow the customer to continue browsing the restaurant menu if the sorting request is unsuccessful.

7. Record the sorting failure event for system monitoring, diagnostics, auditing, and analytics purposes, where applicable.

8. Ensure that no restaurant, menu, food item, or sorting configuration data is modified as a result of the failed sorting request.

9. Maintain the customer's current browsing session and application state unless termination is required due to security or system policies.

#### 3.3.6.13 Acceptance Criteria

The Sort Menu Items functionality shall be considered successfully implemented when all the following conditions are satisfied:

| AC ID | Acceptance Criteria |
|-------|----------------------|
| AC-SRT-001 | The customer shall be able to select a supported sorting option while viewing the restaurant menu. |
| AC-SRT-002 | The system shall apply the selected sorting option only to the latest published menu of the selected restaurant. |
| AC-SRT-003 | The system shall display only active, published, and customer-visible food items in the sorted results. |
| AC-SRT-004 | The system shall arrange the displayed menu items according to the selected sorting criterion. |
| AC-SRT-005 | The system shall preserve any previously applied search keywords and filter criteria while applying the selected sorting option, where applicable. |
| AC-SRT-006 | The customer shall be able to change, replace, or reset the selected sorting option at any time. |
| AC-SRT-007 | The system shall refresh the displayed menu items immediately after the sorting option is updated. |
| AC-SRT-008 | The customer shall be able to select any displayed food item to view its detailed information. |
| AC-SRT-009 | The system shall preserve the platform's default menu ordering when the customer resets the sorting preference. |
| AC-SRT-010 | The system shall display an appropriate message if the sorting request cannot be completed successfully. |
| AC-SRT-011 | The system shall exclude unpublished, deleted, disabled, archived, or unauthorized food items from the sorted results. |
| AC-SRT-012 | The system shall preserve the selected sorting option during the customer's current browsing session unless it is changed, reset, or the customer leaves the restaurant menu. |
| AC-SRT-013 | The system shall provide a consistent, accurate, and responsive sorting experience throughout the customer's session. |

### 3.3.7 View Item Images

#### 3.3.7.1 Description

The View Item Images functionality enables customers to view the images associated with a food item while browsing the restaurant menu. The system shall display the latest approved and customer-visible images for the selected food item, allowing customers to better understand the appearance and presentation of the food before making a purchase decision.

#### 3.3.7.2 Actors

**Primary Actor**

- Customer

**Supporting Actors**

- Menu Service
- Media Management Service
- Restaurant Service
- Authentication and Authorization Service (where applicable)

#### 3.3.7.3 Preconditions

1. The customer shall have access to the QuickBite platform.

2. The selected restaurant shall exist and be available for customer access.

3. The selected food item shall exist within the restaurant's latest published menu.

4. The selected food item shall be active and customer-visible.

5. At least one approved image shall be associated with the selected food item.

6. The customer shall have opened the food item details or menu listing before viewing the item images.

#### 3.3.7.4 Trigger

The use case begins when the customer selects or views the image of a food item from the restaurant menu or food item details page.

#### 3.3.7.5 Input Fields

| Field | Description | Mandatory |
|-------|-------------|-----------|
| Restaurant ID | Unique identifier of the selected restaurant | Yes |
| Food Item ID | Unique identifier of the selected food item | Yes |
| Image ID | Identifier of the selected image, where applicable | No |

#### 3.3.7.6 Business Rules

1. The system shall display only the latest approved images associated with the selected food item.

2. The system shall display only images that are active and customer-visible.

3. The system shall not display images associated with unpublished, deleted, disabled, or unauthorized food items.

4. The system shall support displaying one or more images for a food item, where available.

5. The customer may view images directly from the menu listing or the food item details page.

6. The customer may navigate between multiple images of the selected food item, where multiple images are available.

7. The system shall preserve the original image quality while optimizing image delivery for supported devices and network conditions.

8. The system shall display a platform-defined placeholder image when no approved food item image is available.

9. The system shall not allow customers to modify, upload, download, or delete food item images.

10. The system shall display images in accordance with the platform's content moderation and image visibility policies.

11. The system shall record image viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

12. The system shall ensure that viewing food item images does not modify any restaurant, menu, food item, or image data.

#### 3.3.7.7 Validations

1. The system shall validate that the selected restaurant exists before retrieving the food item images.

2. The system shall validate that the selected food item exists within the restaurant's latest published menu.

3. The system shall validate that the selected food item is active and customer-visible.

4. The system shall validate that the requested image is associated with the selected food item, where a specific image is requested.

5. The system shall validate that the requested image is active, approved, and available for customer viewing.

6. The system shall validate that the customer is authorized to view the selected food item and its associated images, where access restrictions apply.

7. The system shall ensure that unpublished, deleted, disabled, archived, or unauthorized images are not displayed.

8. The system shall validate that the requested image format is supported by the platform before rendering the image.

9. The system shall display a platform-defined placeholder image when no approved image is available for the selected food item.

10. The system shall validate all image retrieval requests before processing them.

11. The system shall ensure that image viewing requests do not modify any restaurant, menu, food item, or image data.

12. The system shall validate that the image resource is available before displaying it to the customer.

#### 3.3.7.8 Main Flow

1. The customer opens the menu or food item details page.

2. The customer selects or taps the food item image.

3. The system receives the image viewing request.

4. The system validates the request.

5. The system retrieves the latest approved and customer-visible images associated with the selected food item.

6. The system verifies that the images are active and authorized for customer viewing.

7. The system optimizes the images for delivery based on the customer's device and supported network conditions, where applicable.

8. The system displays the selected image to the customer.

9. If multiple images are available, the system allows the customer to navigate between the images.

10. The customer views the food item images.

11. The customer may close the image viewer and return to the menu or food item details page.

12. The system records image viewing activity for analytics and reporting purposes.

13. The use case ends successfully.

#### 3.3.7.9 Alternate Flows

##### AF-1: Restaurant Does Not Exist

1. The customer attempts to view a food item image.
2. The system determines that the selected restaurant does not exist.
3. The system displays an appropriate error message indicating that the restaurant could not be found.
4. The use case ends.

---

##### AF-2: Food Item Does Not Exist

1. The customer selects a food item image.
2. The system determines that the selected food item does not exist in the restaurant's latest published menu.
3. The system displays an appropriate error message.
4. The use case ends.

---

##### AF-3: Approved Image Is Not Available

1. The customer attempts to view the food item image.
2. The system determines that no approved customer-visible image is available for the selected food item.
3. The system displays the platform-defined placeholder image.
4. The customer may continue browsing the food item details.
5. The use case continues.

---

##### AF-4: Image Resource Is Unavailable

1. The customer requests to view a food item image.
2. The system determines that the requested image resource cannot be retrieved due to a temporary system or network issue.
3. The system displays an appropriate error message or placeholder image.
4. The customer may retry viewing the image.
5. The use case ends.

---

##### AF-5: Customer Is Not Authorized to View the Image

1. The customer requests to view a food item image.
2. The system determines that the requested image is restricted based on authorization or business policies.
3. The system prevents the image from being displayed.
4. The system displays an appropriate authorization message, where applicable.
5. The use case ends.

---

##### AF-6: Unsupported Image Format

1. The customer requests to view a food item image.
2. The system determines that the image format is not supported by the platform or the customer's device.
3. The system displays an appropriate error message or placeholder image.
4. The customer may continue browsing the food item details.
5. The use case ends.

---

##### AF-7: Multiple Images Are Available

1. The customer opens the food item image viewer.
2. The system determines that multiple approved images are available for the selected food item.
3. The system displays the primary image first.
4. The customer navigates between the available images.
5. The use case continues until the customer closes the image viewer.

#### 3.3.7.10 Postconditions

Upon completion of the View Item Images functionality, one of the following postconditions shall apply:

##### Successful Completion

1. The approved and customer-visible image(s) of the selected food item shall be displayed to the customer.

2. The customer shall be able to view one or more images associated with the selected food item, where available.

3. The customer shall be able to navigate between multiple images, where applicable.

4. The customer shall be able to close the image viewer and continue browsing the restaurant menu or food item details without interruption.

5. The system shall record the customer's image viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

6. No restaurant, menu, food item, or image data shall be modified during the image viewing operation.

##### Unsuccessful Completion

1. The requested food item image shall not be displayed.

2. The system shall notify the customer of the reason the image could not be displayed.

3. The system shall display a platform-defined placeholder image where applicable.

4. The system shall prevent unpublished, deleted, disabled, archived, or unauthorized images from being displayed.

5. No restaurant, menu, food item, or image data shall be modified as a result of the failed image viewing request.

6. The customer's existing browsing session shall remain active unless termination is required due to security or system policies.

#### 3.3.7.11 Success Response

Upon successful completion of the View Item Images functionality, the system shall:

1. Display the latest approved and customer-visible image(s) associated with the selected food item.

2. Display the images in their supported resolution while optimizing delivery for the customer's device and network conditions.

3. Display only active, approved, and authorized images.

4. Allow the customer to navigate between multiple images, where multiple images are available.

5. Allow the customer to zoom or view the image in full-screen mode, where supported by the platform.

6. Display the images without modifying the customer's current browsing context.

7. Allow the customer to close the image viewer and return to the restaurant menu or food item details page.

8. Display a consistent and responsive image viewing experience across supported devices.

9. Record image viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

#### 3.3.7.12 Failure Response

If the View Item Images functionality cannot be completed successfully, the system shall:

1. Inform the customer that the requested food item image could not be displayed.

2. Display an appropriate and user-friendly message describing the reason for the failure, where applicable.

3. Display the platform-defined placeholder image when an approved image is unavailable, where applicable.

4. Prevent the display of unpublished, deleted, disabled, archived, or unauthorized images.

5. Allow the customer to retry viewing the image when the failure is temporary.

6. Allow the customer to continue browsing the restaurant menu or food item details if the image cannot be displayed.

7. Record the image viewing failure event for system monitoring, diagnostics, auditing, and analytics purposes, where applicable.

8. Ensure that no restaurant, menu, food item, or image data is modified as a result of the failed image viewing request.

9. Maintain the customer's current browsing session and application state unless termination is required due to security or system policies.

#### 3.3.7.13 Acceptance Criteria

The View Item Images functionality shall be considered successfully implemented when all the following conditions are satisfied:

| AC ID | Acceptance Criteria |
|-------|----------------------|
| AC-VII-001 | The customer shall be able to view the approved images associated with a selected food item. |
| AC-VII-002 | The system shall display only active, approved, and customer-visible images. |
| AC-VII-003 | The system shall retrieve and display images associated only with the selected food item. |
| AC-VII-004 | The system shall support displaying multiple images for a food item, where available. |
| AC-VII-005 | The customer shall be able to navigate between multiple images without leaving the image viewer. |
| AC-VII-006 | The system shall optimize image delivery for supported devices and network conditions while preserving image quality. |
| AC-VII-007 | The system shall display a platform-defined placeholder image when no approved image is available for the selected food item. |
| AC-VII-008 | The customer shall be able to close the image viewer and return to the restaurant menu or food item details page without losing the current browsing context. |
| AC-VII-009 | The system shall prevent unpublished, deleted, disabled, archived, or unauthorized images from being displayed. |
| AC-VII-010 | The system shall ensure that viewing images does not modify any restaurant, menu, food item, or image data. |
| AC-VII-011 | The system shall display an appropriate error message when an image cannot be retrieved or displayed. |
| AC-VII-012 | The system shall record image viewing activity for analytics and reporting purposes, where applicable. |
| AC-VII-013 | The system shall provide a consistent, accurate, and responsive image viewing experience across supported devices and platforms. |


### 3.3.8 View Item Description

#### 3.3.8.1 Description

The View Item Description functionality enables customers to view the detailed description of a selected food item while browsing the restaurant menu. The system shall display the latest approved and customer-visible description, providing customers with additional information such as the item's ingredients, preparation style, taste profile, serving details, and other relevant information to support informed purchasing decisions.

#### 3.3.8.2 Actors

**Primary Actor**

- Customer

**Supporting Actors**

- Menu Service
- Restaurant Service
- Content Management Service
- Authentication and Authorization Service (where applicable)

#### 3.3.8.3 Preconditions

1. The customer shall have access to the QuickBite platform.

2. The selected restaurant shall exist and be available for customer access.

3. The selected food item shall exist within the restaurant's latest published menu.

4. The selected food item shall be active and customer-visible.

5. An approved item description shall be available for the selected food item.

6. The customer shall have opened the food item details or menu listing before viewing the item description.

#### 3.3.8.4 Trigger

The use case begins when the customer selects a food item or opens the food item details page to view its description.

#### 3.3.8.5 Input Fields

| Field | Description | Mandatory |
|-------|-------------|-----------|
| Restaurant ID | Unique identifier of the selected restaurant | Yes |
| Food Item ID | Unique identifier of the selected food item | Yes |

#### 3.3.8.6 Business Rules

1. The system shall display only the latest approved description associated with the selected food item.

2. The system shall display only descriptions of active and customer-visible food items.

3. The system shall not display descriptions associated with unpublished, deleted, disabled, or unauthorized food items.

4. The system shall display the complete item description in accordance with the platform's content presentation guidelines.

5. The item description may include information such as ingredients, preparation style, taste profile, serving details, and other restaurant-provided information, where available.

6. The system shall preserve the original formatting of the approved item description where supported by the platform.

7. The system shall display a platform-defined default message when an approved item description is unavailable.

8. The customer shall have read-only access to the item description and shall not be permitted to modify its contents.

9. The system shall display the item description in accordance with the platform's content moderation and visibility policies.

10. The system shall ensure that viewing the item description does not modify any restaurant, menu, food item, or description data.

11. The system shall record item description viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

12. The system shall retrieve and display the latest approved description whenever the customer accesses the food item details.

#### 3.3.8.7 Validations

1. The system shall validate that the selected restaurant exists before retrieving the item description.

2. The system shall validate that the selected food item exists within the restaurant's latest published menu.

3. The system shall validate that the selected food item is active and customer-visible.

4. The system shall validate that an approved item description is associated with the selected food item, where available.

5. The system shall validate that the customer is authorized to view the selected food item and its description, where access restrictions apply.

6. The system shall ensure that descriptions of unpublished, deleted, disabled, archived, or unauthorized food items are not displayed.

7. The system shall validate that the description content complies with the platform's content visibility policies before displaying it.

8. The system shall display a platform-defined default message when an approved item description is unavailable.

9. The system shall validate that the description data is available before rendering it to the customer.

10. The system shall validate all item description retrieval requests before processing them.

11. The system shall ensure that viewing the item description does not modify any restaurant, menu, food item, or description data.

12. The system shall validate that the latest approved version of the item description is retrieved and displayed.

#### 3.3.8.8 Main Flow

1. The customer opens the restaurant menu or food item details page.

2. The customer selects a food item to view its description.

3. The system receives the item description request.

4. The system validates the request.

5. The system retrieves the latest approved and customer-visible description associated with the selected food item.

6. The system verifies that the description is active and authorized for customer viewing.

7. The system retrieves the latest approved information related to the selected food item.

8. The system displays the item description to the customer.

9. The customer reviews the item description.

10. The customer may continue browsing the food item details or return to the restaurant menu.

11. The system records item description viewing activity for analytics and reporting purposes.

12. The use case ends successfully.

#### 3.3.8.9 Alternate Flows

##### AF-1: Restaurant Does Not Exist

1. The customer attempts to view a food item's description.
2. The system determines that the selected restaurant does not exist.
3. The system displays an appropriate error message indicating that the restaurant could not be found.
4. The use case ends.

---

##### AF-2: Food Item Does Not Exist

1. The customer selects a food item to view its description.
2. The system determines that the selected food item does not exist in the restaurant's latest published menu.
3. The system displays an appropriate error message.
4. The use case ends.

---

##### AF-3: Approved Item Description Is Not Available

1. The customer requests to view the description of a food item.
2. The system determines that no approved customer-visible description is available for the selected food item.
3. The system displays a platform-defined default message indicating that the description is currently unavailable.
4. The customer may continue browsing the food item details.
5. The use case continues.

---

##### AF-4: Description Service Is Unavailable

1. The customer requests to view the item description.
2. The system is unable to retrieve the description due to a temporary system or service failure.
3. The system displays an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

---

##### AF-5: Customer Is Not Authorized to View the Item Description

1. The customer requests to view the description of a food item.
2. The system determines that the requested description is restricted based on authorization or business policies.
3. The system prevents the description from being displayed.
4. The system displays an appropriate authorization message, where applicable.
5. The use case ends.

---

##### AF-6: Description Content Is Temporarily Unavailable

1. The customer requests to view the item description.
2. The system determines that the description content cannot be retrieved due to a temporary content availability issue.
3. The system displays a platform-defined default message or an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

---

##### AF-7: Food Item Is No Longer Available

1. The customer requests to view the description of a food item.
2. The system determines that the selected food item has become unavailable, unpublished, or disabled.
3. The system prevents the description from being displayed.
4. The system informs the customer that the selected food item is no longer available.
5. The use case ends.

#### 3.3.8.10 Postconditions

Upon completion of the View Item Description functionality, one of the following postconditions shall apply:

##### Successful Completion

1. The latest approved and customer-visible description of the selected food item shall be displayed to the customer.

2. The customer shall be able to review the complete item description.

3. The customer shall be able to continue browsing the food item details or return to the restaurant menu without interruption.

4. The system shall record the customer's item description viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

5. The latest approved description shall remain available for subsequent customer requests until updated by an authorized user.

6. No restaurant, menu, food item, or description data shall be modified during the item description viewing operation.

##### Unsuccessful Completion

1. The requested item description shall not be displayed.

2. The system shall notify the customer of the reason the description could not be displayed.

3. The system shall display a platform-defined default message where an approved item description is unavailable, where applicable.

4. The system shall prevent descriptions of unpublished, deleted, disabled, archived, or unauthorized food items from being displayed.

5. No restaurant, menu, food item, or description data shall be modified as a result of the failed item description viewing request.

6. The customer's existing browsing session shall remain active unless termination is required due to security or system policies.

#### 3.3.8.11 Success Response

Upon successful completion of the View Item Description functionality, the system shall:

1. Display the latest approved and customer-visible description of the selected food item.

2. Display the complete item description in accordance with the platform's content presentation guidelines.

3. Display only descriptions associated with active, published, and customer-visible food items.

4. Preserve the approved formatting of the item description, where supported by the platform.

5. Display any available information such as ingredients, preparation style, taste profile, serving details, and other restaurant-provided information.

6. Allow the customer to continue browsing the food item details or return to the restaurant menu without losing the current browsing context.

7. Display the description without modifying any restaurant, menu, food item, or description data.

8. Provide a consistent, accurate, and responsive description viewing experience across supported devices and platforms.

9. Record item description viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

#### 3.3.8.12 Failure Response

If the View Item Description functionality cannot be completed successfully, the system shall:

1. Inform the customer that the requested item description could not be displayed.

2. Display an appropriate and user-friendly message describing the reason for the failure, where applicable.

3. Display a platform-defined default message when an approved item description is unavailable, where applicable.

4. Prevent the display of descriptions associated with unpublished, deleted, disabled, archived, or unauthorized food items.

5. Allow the customer to retry viewing the item description when the failure is temporary.

6. Allow the customer to continue browsing the restaurant menu or food item details if the description cannot be displayed.

7. Record the item description viewing failure event for system monitoring, diagnostics, auditing, and analytics purposes, where applicable.

8. Ensure that no restaurant, menu, food item, or description data is modified as a result of the failed item description viewing request.

9. Maintain the customer's current browsing session and application state unless termination is required due to security or system policies.

#### 3.3.8.13 Acceptance Criteria

The View Item Description functionality shall be considered successfully implemented when all the following conditions are satisfied:

| AC ID | Acceptance Criteria |
|-------|----------------------|
| AC-VID-001 | The customer shall be able to view the latest approved description of a selected food item. |
| AC-VID-002 | The system shall display only descriptions associated with active, published, and customer-visible food items. |
| AC-VID-003 | The system shall retrieve and display the description associated only with the selected food item. |
| AC-VID-004 | The system shall display the complete approved item description in accordance with the platform's content presentation guidelines. |
| AC-VID-005 | The system shall preserve the approved formatting of the item description, where supported by the platform. |
| AC-VID-006 | The system shall display available information such as ingredients, preparation style, taste profile, serving details, and other restaurant-provided information, where applicable. |
| AC-VID-007 | The system shall display a platform-defined default message when no approved item description is available. |
| AC-VID-008 | The customer shall be able to continue browsing the restaurant menu or food item details without losing the current browsing context. |
| AC-VID-009 | The system shall prevent descriptions of unpublished, deleted, disabled, archived, or unauthorized food items from being displayed. |
| AC-VID-010 | The system shall ensure that viewing the item description does not modify any restaurant, menu, food item, or description data. |
| AC-VID-011 | The system shall display an appropriate error message when the item description cannot be retrieved or displayed. |
| AC-VID-012 | The system shall record item description viewing activity for analytics and reporting purposes, where applicable. |
| AC-VID-013 | The system shall provide a consistent, accurate, and responsive item description viewing experience across supported devices and platforms. |

### 3.3.9 View Ingredients

#### 3.3.9.1 Description

The View Ingredients functionality enables customers to view the list of ingredients used in the preparation of a selected food item. The system shall display the latest approved and customer-visible ingredient information associated with the selected food item, allowing customers to make informed purchasing decisions based on dietary preferences, allergies, nutritional awareness, or personal food choices.

#### 3.3.9.2 Actors

**Primary Actor**

- Customer

**Supporting Actors**

- Menu Service
- Restaurant Service
- Content Management Service
- Authentication and Authorization Service (where applicable)

#### 3.3.9.3 Preconditions

1. The customer shall have access to the QuickBite platform.

2. The selected restaurant shall exist and be available for customer access.

3. The selected food item shall exist within the restaurant's latest published menu.

4. The selected food item shall be active and customer-visible.

5. The selected food item shall have an approved ingredient list, where available.

6. The customer shall have opened the food item details or menu listing before viewing the ingredients.

#### 3.3.9.4 Trigger

The use case begins when the customer selects the option to view the ingredients of a food item from the restaurant menu or food item details page.

#### 3.3.9.5 Input Fields

| Field | Description | Mandatory |
|-------|-------------|-----------|
| Restaurant ID | Unique identifier of the selected restaurant | Yes |
| Food Item ID | Unique identifier of the selected food item | Yes |

#### 3.3.9.6 Business Rules

1. The system shall display only the latest approved ingredient list associated with the selected food item.

2. The system shall display ingredient information only for active and customer-visible food items.

3. The system shall not display ingredient information associated with unpublished, deleted, disabled, or unauthorized food items.

4. The ingredient list shall be displayed in accordance with the platform's content presentation guidelines.

5. The ingredient information may include the primary ingredients, optional ingredients, additives, seasonings, allergens, and other restaurant-provided information, where applicable.

6. The system shall preserve the approved formatting and sequence of the ingredient list where supported by the platform.

7. The system shall display a platform-defined default message when approved ingredient information is unavailable.

8. The customer shall have read-only access to the ingredient information and shall not be permitted to modify its contents.

9. The system shall display ingredient information in accordance with the platform's content moderation and visibility policies.

10. The system shall ensure that viewing ingredient information does not modify any restaurant, menu, food item, or ingredient data.

11. The system shall record ingredient viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

12. The system shall retrieve and display the latest approved ingredient information whenever the customer accesses the food item details or ingredient section.

#### 3.3.9.7 Validations

1. The system shall validate that the selected restaurant exists before retrieving the ingredient information.

2. The system shall validate that the selected food item exists within the restaurant's latest published menu.

3. The system shall validate that the selected food item is active and customer-visible.

4. The system shall validate that approved ingredient information is associated with the selected food item, where available.

5. The system shall validate that the customer is authorized to view the selected food item and its ingredient information, where access restrictions apply.

6. The system shall ensure that ingredient information associated with unpublished, deleted, disabled, archived, or unauthorized food items is not displayed.

7. The system shall validate that the ingredient information complies with the platform's content visibility policies before displaying it.

8. The system shall display a platform-defined default message when approved ingredient information is unavailable.

9. The system shall validate that the ingredient data is available before rendering it to the customer.

10. The system shall validate all ingredient information retrieval requests before processing them.

11. The system shall ensure that viewing ingredient information does not modify any restaurant, menu, food item, or ingredient data.

12. The system shall validate that the latest approved version of the ingredient information is retrieved and displayed.

#### 3.3.9.8 Main Flow

1. The customer opens the restaurant menu or food item details page.

2. The customer selects the option to view the ingredients of a food item.

3. The system receives the ingredient information request.

4. The system validates the request.

5. The system retrieves the latest approved and customer-visible ingredient information associated with the selected food item.

6. The system verifies that the ingredient information is active and authorized for customer viewing.

7. The system retrieves the latest approved ingredient details for the selected food item.

8. The system displays the ingredient information to the customer.

9. The customer reviews the ingredient information.

10. The customer may continue browsing the food item details or return to the restaurant menu.

11. The system records ingredient viewing activity for analytics and reporting purposes.

12. The use case ends successfully.

#### 3.3.9.9 Alternate Flows

##### AF-1: Restaurant Does Not Exist

1. The customer attempts to view the ingredients of a food item.
2. The system determines that the selected restaurant does not exist.
3. The system displays an appropriate error message indicating that the restaurant could not be found.
4. The use case ends.

---

##### AF-2: Food Item Does Not Exist

1. The customer selects a food item to view its ingredients.
2. The system determines that the selected food item does not exist in the restaurant's latest published menu.
3. The system displays an appropriate error message.
4. The use case ends.

---

##### AF-3: Approved Ingredient Information Is Not Available

1. The customer requests to view the ingredients of a food item.
2. The system determines that no approved customer-visible ingredient information is available for the selected food item.
3. The system displays a platform-defined default message indicating that the ingredient information is currently unavailable.
4. The customer may continue browsing the food item details.
5. The use case continues.

---

##### AF-4: Ingredient Information Service Is Unavailable

1. The customer requests to view the ingredient information.
2. The system is unable to retrieve the ingredient information due to a temporary system or service failure.
3. The system displays an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

---

##### AF-5: Customer Is Not Authorized to View the Ingredient Information

1. The customer requests to view the ingredients of a food item.
2. The system determines that the requested ingredient information is restricted based on authorization or business policies.
3. The system prevents the ingredient information from being displayed.
4. The system displays an appropriate authorization message, where applicable.
5. The use case ends.

---

##### AF-6: Ingredient Information Is Temporarily Unavailable

1. The customer requests to view the ingredient information.
2. The system determines that the ingredient information cannot be retrieved due to a temporary content availability issue.
3. The system displays a platform-defined default message or an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

---

##### AF-7: Food Item Is No Longer Available

1. The customer requests to view the ingredients of a food item.
2. The system determines that the selected food item has become unavailable, unpublished, or disabled.
3. The system prevents the ingredient information from being displayed.
4. The system informs the customer that the selected food item is no longer available.
5. The use case ends.

#### 3.3.9.10 Postconditions

Upon completion of the View Ingredients functionality, one of the following postconditions shall apply:

##### Successful Completion

1. The latest approved and customer-visible ingredient information of the selected food item shall be displayed to the customer.

2. The customer shall be able to review the complete ingredient list associated with the selected food item.

3. The customer shall be able to continue browsing the food item details or return to the restaurant menu without interruption.

4. The system shall record the customer's ingredient viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

5. The latest approved ingredient information shall remain available for subsequent customer requests until updated by an authorized user.

6. No restaurant, menu, food item, or ingredient data shall be modified during the ingredient viewing operation.

##### Unsuccessful Completion

1. The requested ingredient information shall not be displayed.

2. The system shall notify the customer of the reason the ingredient information could not be displayed.

3. The system shall display a platform-defined default message where approved ingredient information is unavailable, where applicable.

4. The system shall prevent ingredient information associated with unpublished, deleted, disabled, archived, or unauthorized food items from being displayed.

5. No restaurant, menu, food item, or ingredient data shall be modified as a result of the failed ingredient viewing request.

6. The customer's existing browsing session shall remain active unless termination is required due to security or system policies.

#### 3.3.9.11 Success Response

Upon successful completion of the View Ingredients functionality, the system shall:

1. Display the latest approved and customer-visible ingredient information associated with the selected food item.

2. Display the complete ingredient list in accordance with the platform's content presentation guidelines.

3. Display only ingredient information associated with active, published, and customer-visible food items.

4. Preserve the approved formatting and sequence of the ingredient information, where supported by the platform.

5. Display available information such as primary ingredients, optional ingredients, additives, seasonings, allergens, and other restaurant-provided information, where applicable.

6. Allow the customer to continue browsing the food item details or return to the restaurant menu without losing the current browsing context.

7. Display the ingredient information without modifying any restaurant, menu, food item, or ingredient data.

8. Provide a consistent, accurate, and responsive ingredient viewing experience across supported devices and platforms.

9. Record ingredient viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

#### 3.3.9.12 Failure Response

If the View Ingredients functionality cannot be completed successfully, the system shall:

1. Inform the customer that the requested ingredient information could not be displayed.

2. Display an appropriate and user-friendly message describing the reason for the failure, where applicable.

3. Display a platform-defined default message when approved ingredient information is unavailable, where applicable.

4. Prevent the display of ingredient information associated with unpublished, deleted, disabled, archived, or unauthorized food items.

5. Allow the customer to retry viewing the ingredient information when the failure is temporary.

6. Allow the customer to continue browsing the restaurant menu or food item details if the ingredient information cannot be displayed.

7. Record the ingredient viewing failure event for system monitoring, diagnostics, auditing, and analytics purposes, where applicable.

8. Ensure that no restaurant, menu, food item, or ingredient data is modified as a result of the failed ingredient viewing request.

9. Maintain the customer's current browsing session and application state unless termination is required due to security or system policies.

#### 3.3.9.13 Acceptance Criteria

The View Ingredients functionality shall be considered successfully implemented when all the following conditions are satisfied:

| AC ID | Acceptance Criteria |
|-------|----------------------|
| AC-VIG-001 | The customer shall be able to view the latest approved ingredient information associated with a selected food item. |
| AC-VIG-002 | The system shall display only ingredient information associated with active, published, and customer-visible food items. |
| AC-VIG-003 | The system shall retrieve and display the ingredient information associated only with the selected food item. |
| AC-VIG-004 | The system shall display the complete approved ingredient list in accordance with the platform's content presentation guidelines. |
| AC-VIG-005 | The system shall preserve the approved formatting and sequence of the ingredient information, where supported by the platform. |
| AC-VIG-006 | The system shall display available information such as primary ingredients, optional ingredients, additives, seasonings, allergens, and other restaurant-provided information, where applicable. |
| AC-VIG-007 | The system shall display a platform-defined default message when no approved ingredient information is available. |
| AC-VIG-008 | The customer shall be able to continue browsing the restaurant menu or food item details without losing the current browsing context. |
| AC-VIG-009 | The system shall prevent ingredient information associated with unpublished, deleted, disabled, archived, or unauthorized food items from being displayed. |
| AC-VIG-010 | The system shall ensure that viewing ingredient information does not modify any restaurant, menu, food item, or ingredient data. |
| AC-VIG-011 | The system shall display an appropriate error message when the ingredient information cannot be retrieved or displayed. |
| AC-VIG-012 | The system shall record ingredient viewing activity for analytics and reporting purposes, where applicable. |
| AC-VIG-013 | The system shall provide a consistent, accurate, and responsive ingredient viewing experience across supported devices and platforms. |

### 3.3.10 View Nutritional Information

#### 3.3.10.1 Description

The View Nutritional Information functionality enables customers to view the nutritional details of a selected food item while browsing the restaurant menu. The system shall display the latest approved and customer-visible nutritional information associated with the selected food item, allowing customers to make informed purchasing decisions based on their dietary preferences, health goals, medical requirements, or nutritional awareness.

#### 3.3.10.2 Actors

**Primary Actor**

- Customer

**Supporting Actors**

- Menu Service
- Restaurant Service
- Nutrition Information Service
- Authentication and Authorization Service (where applicable)

#### 3.3.10.3 Preconditions

1. The customer shall have access to the QuickBite platform.

2. The selected restaurant shall exist and be available for customer access.

3. The selected food item shall exist within the restaurant's latest published menu.

4. The selected food item shall be active and customer-visible.

5. Approved nutritional information shall be available for the selected food item, where applicable.

6. The customer shall have opened the food item details or menu listing before viewing the nutritional information.

#### 3.3.10.4 Trigger

The use case begins when the customer selects the option to view the nutritional information of a food item from the restaurant menu or food item details page.

#### 3.3.10.5 Input Fields

| Field | Description | Mandatory |
|-------|-------------|-----------|
| Restaurant ID | Unique identifier of the selected restaurant | Yes |
| Food Item ID | Unique identifier of the selected food item | Yes |

#### 3.3.10.6 Business Rules

1. The system shall display only the latest approved and customer-visible nutritional information associated with the selected food item.

2. Nutritional information shall be displayed only for active, published, and customer-visible food items.

3. The system shall retrieve nutritional information only for the selected food item.

4. The displayed nutritional information shall reflect the latest published version available in the system.

5. Nutritional information shall be presented in a clear, consistent, and standardized format across the platform.

6. The system shall display only nutritional information approved for customer visibility.

7. Nutritional information may include, where available:
   - Serving Size
   - Calories
   - Total Fat
   - Saturated Fat
   - Trans Fat
   - Cholesterol
   - Sodium
   - Total Carbohydrates
   - Dietary Fiber
   - Total Sugars
   - Added Sugars
   - Protein
   - Vitamins
   - Minerals
   - Other restaurant-provided nutritional details

8. The system shall display nutritional values together with their applicable measurement units.

9. If approved nutritional information is unavailable, the system shall display a platform-defined default message.

10. The system shall not estimate, calculate, or generate nutritional information that has not been approved by the restaurant or platform.

11. Viewing nutritional information shall be a read-only operation and shall not modify any restaurant, menu, food item, or nutritional data.

12. The system shall record nutritional information viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

13. The system shall comply with applicable food labeling, nutritional disclosure, privacy, and regulatory requirements, where applicable.

#### 3.3.10.7 Validations

1. The system shall validate that the selected restaurant exists.

2. The system shall validate that the selected food item exists within the restaurant's latest published menu.

3. The system shall validate that the selected food item is active, published, and customer-visible.

4. The system shall validate that the nutritional information is associated with the selected food item.

5. The system shall validate that only the latest approved nutritional information is displayed.

6. The system shall validate that the nutritional information is approved for customer visibility before displaying it.

7. The system shall validate that all nutritional values displayed correspond to the latest published version of the selected food item.

8. The system shall validate that nutritional measurement units are available and displayed correctly, where applicable.

9. The system shall validate that restricted, unpublished, deleted, disabled, or archived nutritional information is not displayed to customers.

10. The system shall validate that the customer has permission to access the nutritional information where authorization policies apply.

11. The system shall validate system availability before retrieving the nutritional information.

12. The system shall validate that the retrieved nutritional information is complete and not corrupted before displaying it to the customer.

13. The system shall display a platform-defined default message if approved nutritional information is unavailable.

14. The system shall validate that the nutritional information viewing request does not modify any restaurant, menu, food item, or nutritional data.

#### 3.3.10.8 Main Flow

1. The customer selects a food item from the restaurant menu or food item details page.

2. The customer requests to view the nutritional information of the selected food item.

3. The system validates that the selected restaurant exists.

4. The system validates that the selected food item exists within the restaurant's latest published menu.

5. The system validates that the selected food item is active, published, and customer-visible.

6. The system validates that approved nutritional information is available for the selected food item.

7. The system retrieves the latest approved nutritional information associated with the selected food item.

8. The system validates that the retrieved nutritional information is approved for customer visibility.

9. The system displays the nutritional information in a standardized and customer-friendly format.

10. The system displays available nutritional details, where applicable, including serving size, calories, total fat, saturated fat, trans fat, cholesterol, sodium, total carbohydrates, dietary fiber, total sugars, added sugars, protein, vitamins, minerals, and other restaurant-provided nutritional information.

11. The customer reviews the nutritional information.

12. The system records the nutritional information viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

13. The customer continues browsing the food item details or returns to the restaurant menu.

14. The use case ends successfully.

#### 3.3.10.9 Alternate Flows

##### AF-1: Restaurant Does Not Exist

1. The customer attempts to view the nutritional information of a food item.
2. The system determines that the selected restaurant does not exist.
3. The system displays an appropriate error message indicating that the restaurant could not be found.
4. The use case ends.

---

##### AF-2: Food Item Does Not Exist

1. The customer selects a food item to view its nutritional information.
2. The system determines that the selected food item does not exist in the restaurant's latest published menu.
3. The system displays an appropriate error message.
4. The use case ends.

---

##### AF-3: Approved Nutritional Information Is Not Available

1. The customer requests to view the nutritional information of a food item.
2. The system determines that no approved customer-visible nutritional information is available for the selected food item.
3. The system displays a platform-defined default message indicating that the nutritional information is currently unavailable.
4. The customer may continue browsing the food item details.
5. The use case continues.

---

##### AF-4: Nutritional Information Service Is Unavailable

1. The customer requests to view the nutritional information.
2. The system is unable to retrieve the nutritional information due to a temporary system or service failure.
3. The system displays an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

---

##### AF-5: Customer Is Not Authorized to View the Nutritional Information

1. The customer requests to view the nutritional information of a food item.
2. The system determines that the requested nutritional information is restricted based on authorization or business policies.
3. The system prevents the nutritional information from being displayed.
4. The system displays an appropriate authorization message, where applicable.
5. The use case ends.

---

##### AF-6: Nutritional Information Is Temporarily Unavailable

1. The customer requests to view the nutritional information.
2. The system determines that the nutritional information cannot be retrieved due to a temporary content availability issue.
3. The system displays a platform-defined default message or an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

---

##### AF-7: Food Item Is No Longer Available

1. The customer requests to view the nutritional information of a food item.
2. The system determines that the selected food item has become unavailable, unpublished, or disabled.
3. The system prevents the nutritional information from being displayed.
4. The system informs the customer that the selected food item is no longer available.
5. The use case ends.

#### 3.3.10.10 Postconditions

Upon completion of the View Nutritional Information functionality, one of the following postconditions shall apply:

##### Successful Completion

1. The latest approved and customer-visible nutritional information of the selected food item shall be displayed to the customer.

2. The customer shall be able to review the nutritional details associated with the selected food item.

3. The customer shall be able to continue browsing the food item details or return to the restaurant menu without interruption.

4. The system shall record the customer's nutritional information viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

5. The latest approved nutritional information shall remain available for subsequent customer requests until updated by an authorized user.

6. No restaurant, menu, food item, or nutritional data shall be modified during the nutritional information viewing operation.

##### Unsuccessful Completion

1. The requested nutritional information shall not be displayed.

2. The system shall notify the customer of the reason the nutritional information could not be displayed.

3. The system shall display a platform-defined default message where approved nutritional information is unavailable, where applicable.

4. The system shall prevent nutritional information associated with unpublished, deleted, disabled, archived, or unauthorized food items from being displayed.

5. No restaurant, menu, food item, or nutritional data shall be modified as a result of the failed nutritional information viewing request.

6. The customer's existing browsing session shall remain active unless termination is required due to security or system policies.

#### 3.3.10.11 Success Response

Upon successful completion of the View Nutritional Information functionality, the system shall:

1. Display the latest approved and customer-visible nutritional information associated with the selected food item.

2. Display the nutritional information in a clear, consistent, and standardized format.

3. Display only nutritional information associated with active, published, and customer-visible food items.

4. Preserve the approved formatting, structure, and sequence of the nutritional information, where supported by the platform.

5. Display available nutritional details, where applicable, including serving size, calories, total fat, saturated fat, trans fat, cholesterol, sodium, total carbohydrates, dietary fiber, total sugars, added sugars, protein, vitamins, minerals, and other restaurant-provided nutritional information.

6. Display all nutritional values together with their applicable measurement units.

7. Allow the customer to continue browsing the food item details or return to the restaurant menu without losing the current browsing context.

8. Display the nutritional information without modifying any restaurant, menu, food item, or nutritional data.

9. Provide a consistent, accurate, and responsive nutritional information viewing experience across supported devices and platforms.

10. Record nutritional information viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

#### 3.3.10.12 Failure Response

If the View Nutritional Information functionality cannot be completed successfully, the system shall:

1. Inform the customer that the requested nutritional information could not be displayed.

2. Display an appropriate and user-friendly message describing the reason for the failure, where applicable.

3. Display a platform-defined default message when approved nutritional information is unavailable, where applicable.

4. Prevent the display of nutritional information associated with unpublished, deleted, disabled, archived, or unauthorized food items.

5. Allow the customer to retry viewing the nutritional information when the failure is temporary.

6. Allow the customer to continue browsing the restaurant menu or food item details if the nutritional information cannot be displayed.

7. Record the nutritional information viewing failure event for system monitoring, diagnostics, auditing, and analytics purposes, where applicable.

8. Ensure that no restaurant, menu, food item, or nutritional data is modified as a result of the failed nutritional information viewing request.

9. Maintain the customer's current browsing session and application state unless termination is required due to security or system policies.

#### 3.3.10.13 Acceptance Criteria

The View Nutritional Information functionality shall be considered successfully implemented when all the following conditions are satisfied:

| AC ID | Acceptance Criteria |
|-------|----------------------|
| AC-VNI-001 | The customer shall be able to view the latest approved nutritional information associated with a selected food item. |
| AC-VNI-002 | The system shall display only nutritional information associated with active, published, and customer-visible food items. |
| AC-VNI-003 | The system shall retrieve and display the nutritional information associated only with the selected food item. |
| AC-VNI-004 | The system shall display the complete approved nutritional information in accordance with the platform's content presentation guidelines. |
| AC-VNI-005 | The system shall preserve the approved formatting, structure, and sequence of the nutritional information, where supported by the platform. |
| AC-VNI-006 | The system shall display available nutritional details including serving size, calories, total fat, saturated fat, trans fat, cholesterol, sodium, total carbohydrates, dietary fiber, total sugars, added sugars, protein, vitamins, minerals, and other restaurant-provided nutritional information, where applicable. |
| AC-VNI-007 | The system shall display nutritional values together with their applicable measurement units. |
| AC-VNI-008 | The system shall display a platform-defined default message when approved nutritional information is unavailable. |
| AC-VNI-009 | The customer shall be able to continue browsing the restaurant menu or food item details without losing the current browsing context. |
| AC-VNI-010 | The system shall prevent nutritional information associated with unpublished, deleted, disabled, archived, or unauthorized food items from being displayed. |
| AC-VNI-011 | The system shall ensure that viewing nutritional information does not modify any restaurant, menu, food item, or nutritional data. |
| AC-VNI-012 | The system shall display an appropriate error message when the nutritional information cannot be retrieved or displayed. |
| AC-VNI-013 | The system shall record nutritional information viewing activity for analytics and reporting purposes, where applicable. |
| AC-VNI-014 | The system shall provide a consistent, accurate, and responsive nutritional information viewing experience across supported devices and platforms. |

### 3.3.11 View Allergen Information

#### 3.3.11.1 Description

The View Allergen Information functionality enables customers to view the allergen details of a selected food item while browsing the restaurant menu. The system shall display the latest approved and customer-visible allergen information associated with the selected food item, allowing customers to identify potential allergens and make informed purchasing decisions based on their dietary restrictions, allergies, intolerances, or medical requirements.

#### 3.3.11.2 Actors

**Primary Actor**

- Customer

**Supporting Actors**

- Menu Service
- Restaurant Service
- Allergen Information Service
- Authentication and Authorization Service (where applicable)

#### 3.3.11.3 Preconditions

1. The customer shall have access to the QuickBite platform.

2. The selected restaurant shall exist and be available for customer access.

3. The selected food item shall exist within the restaurant's latest published menu.

4. The selected food item shall be active and customer-visible.

5. Approved allergen information shall be available for the selected food item, where applicable.

6. The customer shall have opened the food item details or menu listing before viewing the allergen information.

#### 3.3.11.4 Trigger

The use case begins when the customer selects the option to view the allergen information of a food item from the restaurant menu or food item details page.

#### 3.3.11.5 Input Fields

| Field | Description | Mandatory |
|-------|-------------|-----------|
| Restaurant ID | Unique identifier of the selected restaurant | Yes |
| Food Item ID | Unique identifier of the selected food item | Yes |

#### 3.3.11.6 Business Rules

1. The system shall display only the latest approved and customer-visible allergen information associated with the selected food item.

2. Allergen information shall be displayed only for active, published, and customer-visible food items.

3. The system shall retrieve allergen information only for the selected food item.

4. The displayed allergen information shall reflect the latest published version available in the system.

5. Allergen information shall be presented in a clear, consistent, and standardized format across the platform.

6. The system shall display only allergen information approved for customer visibility.

7. Allergen information may include, where available:
   - Milk
   - Eggs
   - Fish
   - Shellfish
   - Tree Nuts
   - Peanuts
   - Wheat
   - Soy
   - Sesame
   - Gluten
   - Mustard
   - Celery
   - Lupin
   - Sulphites
   - Molluscs
   - Other restaurant-provided allergen information

8. The system shall clearly distinguish allergens that are present, may be present due to cross-contamination, or are declared by the restaurant, where applicable.

9. If approved allergen information is unavailable, the system shall display a platform-defined default message.

10. The system shall not estimate, infer, or generate allergen information that has not been approved by the restaurant or platform.

11. Viewing allergen information shall be a read-only operation and shall not modify any restaurant, menu, food item, or allergen data.

12. The system shall record allergen information viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

13. The system shall comply with applicable food safety, allergen labeling, privacy, and regulatory requirements, where applicable.

#### 3.3.11.7 Validations

1. The system shall validate that the selected restaurant exists.

2. The system shall validate that the selected food item exists within the restaurant's latest published menu.

3. The system shall validate that the selected food item is active, published, and customer-visible.

4. The system shall validate that the allergen information is associated with the selected food item.

5. The system shall validate that only the latest approved allergen information is displayed.

6. The system shall validate that the allergen information is approved for customer visibility before displaying it.

7. The system shall validate that all displayed allergen information corresponds to the latest published version of the selected food item.

8. The system shall validate that allergen classifications and labels are displayed accurately and consistently, where applicable.

9. The system shall validate that restricted, unpublished, deleted, disabled, or archived allergen information is not displayed to customers.

10. The system shall validate that the customer has permission to access the allergen information where authorization policies apply.

11. The system shall validate system availability before retrieving the allergen information.

12. The system shall validate that the retrieved allergen information is complete and not corrupted before displaying it to the customer.

13. The system shall display a platform-defined default message if approved allergen information is unavailable.

14. The system shall validate that the allergen information viewing request does not modify any restaurant, menu, food item, or allergen data.

#### 3.3.11.8 Main Flow

1. The customer selects a food item from the restaurant menu or food item details page.

2. The customer requests to view the allergen information of the selected food item.

3. The system validates that the selected restaurant exists.

4. The system validates that the selected food item exists within the restaurant's latest published menu.

5. The system validates that the selected food item is active, published, and customer-visible.

6. The system validates that approved allergen information is available for the selected food item.

7. The system retrieves the latest approved allergen information associated with the selected food item.

8. The system validates that the retrieved allergen information is approved for customer visibility.

9. The system displays the allergen information in a standardized and customer-friendly format.

10. The system displays available allergen details, where applicable, including allergens that are present, may be present due to cross-contamination, or are declared by the restaurant.

11. The customer reviews the allergen information.

12. The system records the allergen information viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

13. The customer continues browsing the food item details or returns to the restaurant menu.

14. The use case ends successfully.

#### 3.3.11.9 Alternate Flows

##### AF-1: Restaurant Does Not Exist

1. The customer attempts to view the allergen information of a food item.
2. The system determines that the selected restaurant does not exist.
3. The system displays an appropriate error message indicating that the restaurant could not be found.
4. The use case ends.

---

##### AF-2: Food Item Does Not Exist

1. The customer selects a food item to view its allergen information.
2. The system determines that the selected food item does not exist in the restaurant's latest published menu.
3. The system displays an appropriate error message.
4. The use case ends.

---

##### AF-3: Approved Allergen Information Is Not Available

1. The customer requests to view the allergen information of a food item.
2. The system determines that no approved customer-visible allergen information is available for the selected food item.
3. The system displays a platform-defined default message indicating that the allergen information is currently unavailable.
4. The customer may continue browsing the food item details.
5. The use case continues.

---

##### AF-4: Allergen Information Service Is Unavailable

1. The customer requests to view the allergen information.
2. The system is unable to retrieve the allergen information due to a temporary system or service failure.
3. The system displays an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

---

##### AF-5: Customer Is Not Authorized to View the Allergen Information

1. The customer requests to view the allergen information of a food item.
2. The system determines that the requested allergen information is restricted based on authorization or business policies.
3. The system prevents the allergen information from being displayed.
4. The system displays an appropriate authorization message, where applicable.
5. The use case ends.

---

##### AF-6: Allergen Information Is Temporarily Unavailable

1. The customer requests to view the allergen information.
2. The system determines that the allergen information cannot be retrieved due to a temporary content availability issue.
3. The system displays a platform-defined default message or an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

---

##### AF-7: Food Item Is No Longer Available

1. The customer requests to view the allergen information of a food item.
2. The system determines that the selected food item has become unavailable, unpublished, or disabled.
3. The system prevents the allergen information from being displayed.
4. The system informs the customer that the selected food item is no longer available.
5. The use case ends.

#### 3.3.11.10 Postconditions

Upon completion of the View Allergen Information functionality, one of the following postconditions shall apply:

##### Successful Completion

1. The latest approved and customer-visible allergen information of the selected food item shall be displayed to the customer.

2. The customer shall be able to review the allergen details associated with the selected food item.

3. The customer shall be able to continue browsing the food item details or return to the restaurant menu without interruption.

4. The system shall record the customer's allergen information viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

5. The latest approved allergen information shall remain available for subsequent customer requests until updated by an authorized user.

6. No restaurant, menu, food item, or allergen data shall be modified during the allergen information viewing operation.

##### Unsuccessful Completion

1. The requested allergen information shall not be displayed.

2. The system shall notify the customer of the reason the allergen information could not be displayed.

3. The system shall display a platform-defined default message where approved allergen information is unavailable, where applicable.

4. The system shall prevent allergen information associated with unpublished, deleted, disabled, archived, or unauthorized food items from being displayed.

5. No restaurant, menu, food item, or allergen data shall be modified as a result of the failed allergen information viewing request.

6. The customer's existing browsing session shall remain active unless termination is required due to security or system policies.

#### 3.3.11.11 Success Response

Upon successful completion of the View Allergen Information functionality, the system shall:

1. Display the latest approved and customer-visible allergen information associated with the selected food item.

2. Display the allergen information in a clear, consistent, and standardized format.

3. Display only allergen information associated with active, published, and customer-visible food items.

4. Preserve the approved formatting, structure, and sequence of the allergen information, where supported by the platform.

5. Display available allergen details, where applicable, including allergens that are present, may be present due to cross-contamination, or are declared by the restaurant.

6. Clearly distinguish confirmed allergens from advisory allergen warnings, where applicable.

7. Allow the customer to continue browsing the food item details or return to the restaurant menu without losing the current browsing context.

8. Display the allergen information without modifying any restaurant, menu, food item, or allergen data.

9. Provide a consistent, accurate, and responsive allergen information viewing experience across supported devices and platforms.

10. Record allergen information viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

#### 3.3.11.12 Failure Response

If the View Allergen Information functionality cannot be completed successfully, the system shall:

1. Inform the customer that the requested allergen information could not be displayed.

2. Display an appropriate and user-friendly message describing the reason for the failure, where applicable.

3. Display a platform-defined default message when approved allergen information is unavailable, where applicable.

4. Prevent the display of allergen information associated with unpublished, deleted, disabled, archived, or unauthorized food items.

5. Allow the customer to retry viewing the allergen information when the failure is temporary.

6. Allow the customer to continue browsing the restaurant menu or food item details if the allergen information cannot be displayed.

7. Record the allergen information viewing failure event for system monitoring, diagnostics, auditing, and analytics purposes, where applicable.

8. Ensure that no restaurant, menu, food item, or allergen data is modified as a result of the failed allergen information viewing request.

9. Maintain the customer's current browsing session and application state unless termination is required due to security or system policies.

#### 3.3.11.13 Acceptance Criteria

The View Allergen Information functionality shall be considered successfully implemented when all the following conditions are satisfied:

| AC ID | Acceptance Criteria |
|-------|----------------------|
| AC-VAI-001 | The customer shall be able to view the latest approved allergen information associated with a selected food item. |
| AC-VAI-002 | The system shall display only allergen information associated with active, published, and customer-visible food items. |
| AC-VAI-003 | The system shall retrieve and display the allergen information associated only with the selected food item. |
| AC-VAI-004 | The system shall display the complete approved allergen information in accordance with the platform's content presentation guidelines. |
| AC-VAI-005 | The system shall preserve the approved formatting, structure, and sequence of the allergen information, where supported by the platform. |
| AC-VAI-006 | The system shall display available allergen details including allergens that are present, may be present due to cross-contamination, declared by the restaurant, and other approved allergen information, where applicable. |
| AC-VAI-007 | The system shall clearly distinguish confirmed allergens from advisory allergen warnings, where applicable. |
| AC-VAI-008 | The system shall display a platform-defined default message when approved allergen information is unavailable. |
| AC-VAI-009 | The customer shall be able to continue browsing the restaurant menu or food item details without losing the current browsing context. |
| AC-VAI-010 | The system shall prevent allergen information associated with unpublished, deleted, disabled, archived, or unauthorized food items from being displayed. |
| AC-VAI-011 | The system shall ensure that viewing allergen information does not modify any restaurant, menu, food item, or allergen data. |
| AC-VAI-012 | The system shall display an appropriate error message when the allergen information cannot be retrieved or displayed. |
| AC-VAI-013 | The system shall record allergen information viewing activity for analytics and reporting purposes, where applicable. |
| AC-VAI-014 | The system shall provide a consistent, accurate, and responsive allergen information viewing experience across supported devices and platforms. |

### 3.3.12 View Food Price

#### 3.3.12.1 Description

The View Food Price functionality enables customers to view the current selling price of a selected food item while browsing the restaurant menu. The system shall display the latest approved and customer-visible pricing information associated with the selected food item, allowing customers to make informed purchasing decisions before adding the item to the cart or placing an order.

#### 3.3.12.2 Actors

**Primary Actor**

- Customer

**Supporting Actors**

- Menu Service
- Restaurant Service
- Pricing Service
- Authentication and Authorization Service (where applicable)

#### 3.3.12.3 Preconditions

1. The customer shall have access to the QuickBite platform.

2. The selected restaurant shall exist and be available for customer access.

3. The selected food item shall exist within the restaurant's latest published menu.

4. The selected food item shall be active and customer-visible.

5. Approved pricing information shall be available for the selected food item.

6. The customer shall have opened the restaurant menu or food item details before viewing the food price.

#### 3.3.12.4 Trigger

The use case begins when the customer views a food item from the restaurant menu or food item details page and requests or accesses its pricing information.

#### 3.3.12.5 Input Fields

| Field | Description | Mandatory |
|-------|-------------|-----------|
| Restaurant ID | Unique identifier of the selected restaurant | Yes |
| Food Item ID | Unique identifier of the selected food item | Yes |

#### 3.3.12.6 Business Rules

1. The system shall display only the latest approved and customer-visible price associated with the selected food item.

2. Food prices shall be displayed only for active, published, and customer-visible food items.

3. The system shall retrieve the price only for the selected food item.

4. The displayed price shall reflect the latest published selling price available in the system.

5. The system shall display the price in the platform-supported currency based on applicable business and regional configuration.

6. The displayed price shall include the base selling price of the food item.

7. Where applicable, the system shall additionally display:
   - Original Price
   - Discount Amount
   - Discount Percentage
   - Final Selling Price
   - Applicable Taxes
   - Service Charges
   - Other platform-approved pricing information

8. The system shall clearly distinguish the original price from the discounted selling price, where applicable.

9. The system shall not calculate, estimate, or display prices that have not been approved by the restaurant or platform pricing policies.

10. If approved pricing information is unavailable, the system shall display a platform-defined default message.

11. Viewing food prices shall be a read-only operation and shall not modify any restaurant, menu, food item, pricing, or promotional data.

12. The system shall record food price viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

13. The system shall comply with applicable pricing, taxation, consumer protection, and regulatory requirements, where applicable.

#### 3.3.12.7 Validations

1. The system shall validate that the selected restaurant exists.

2. The system shall validate that the selected food item exists within the restaurant's latest published menu.

3. The system shall validate that the selected food item is active, published, and customer-visible.

4. The system shall validate that the pricing information is associated with the selected food item.

5. The system shall validate that only the latest approved pricing information is displayed.

6. The system shall validate that the displayed price reflects the latest published selling price of the selected food item.

7. The system shall validate that all displayed pricing components, including discounts, taxes, service charges, and final selling price, are approved and applicable, where supported.

8. The system shall validate that the displayed currency complies with the platform's configured regional settings.

9. The system shall validate that restricted, unpublished, deleted, disabled, or archived pricing information is not displayed to customers.

10. The system shall validate that the customer has permission to access the pricing information where authorization policies apply.

11. The system shall validate system availability before retrieving the pricing information.

12. The system shall validate that the retrieved pricing information is complete, accurate, and not corrupted before displaying it to the customer.

13. The system shall display a platform-defined default message if approved pricing information is unavailable.

14. The system shall validate that the food price viewing request does not modify any restaurant, menu, food item, pricing, or promotional data.

#### 3.3.12.8 Main Flow

1. The customer selects a food item from the restaurant menu or food item details page.

2. The customer requests to view the price of the selected food item or the system automatically displays the price as part of the food item details.

3. The system validates that the selected restaurant exists.

4. The system validates that the selected food item exists within the restaurant's latest published menu.

5. The system validates that the selected food item is active, published, and customer-visible.

6. The system validates that approved pricing information is available for the selected food item.

7. The system retrieves the latest approved pricing information associated with the selected food item.

8. The system validates that the retrieved pricing information is approved for customer visibility.

9. The system displays the current selling price of the selected food item.

10. Where applicable, the system additionally displays the original price, discount amount, discount percentage, applicable taxes, service charges, final selling price, and other platform-approved pricing information.

11. The customer reviews the displayed pricing information.

12. The system records the food price viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

13. The customer continues browsing the food item details, restaurant menu, or proceeds to add the item to the cart.

14. The use case ends successfully.

#### 3.3.12.9 Alternate Flows

##### AF-1: Restaurant Does Not Exist

1. The customer attempts to view the price of a food item.
2. The system determines that the selected restaurant does not exist.
3. The system displays an appropriate error message indicating that the restaurant could not be found.
4. The use case ends.

---

##### AF-2: Food Item Does Not Exist

1. The customer selects a food item to view its price.
2. The system determines that the selected food item does not exist in the restaurant's latest published menu.
3. The system displays an appropriate error message.
4. The use case ends.

---

##### AF-3: Approved Pricing Information Is Not Available

1. The customer requests to view the price of a food item.
2. The system determines that no approved customer-visible pricing information is available for the selected food item.
3. The system displays a platform-defined default message indicating that the pricing information is currently unavailable.
4. The customer may continue browsing the food item details.
5. The use case continues.

---

##### AF-4: Pricing Service Is Unavailable

1. The customer requests to view the food price.
2. The system is unable to retrieve the pricing information due to a temporary system or service failure.
3. The system displays an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

---

##### AF-5: Customer Is Not Authorized to View the Pricing Information

1. The customer requests to view the price of a food item.
2. The system determines that the requested pricing information is restricted based on authorization or business policies.
3. The system prevents the pricing information from being displayed.
4. The system displays an appropriate authorization message, where applicable.
5. The use case ends.

---

##### AF-6: Pricing Information Is Temporarily Unavailable

1. The customer requests to view the food price.
2. The system determines that the pricing information cannot be retrieved due to a temporary content availability issue.
3. The system displays a platform-defined default message or an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

---

##### AF-7: Food Item Is No Longer Available

1. The customer requests to view the price of a food item.
2. The system determines that the selected food item has become unavailable, unpublished, or disabled.
3. The system prevents the pricing information from being displayed.
4. The system informs the customer that the selected food item is no longer available.
5. The use case ends.

#### 3.3.12.10 Postconditions

Upon completion of the View Food Price functionality, one of the following postconditions shall apply:

##### Successful Completion

1. The latest approved and customer-visible price of the selected food item shall be displayed to the customer.

2. The customer shall be able to review the pricing details associated with the selected food item.

3. The customer shall be able to continue browsing the food item details, restaurant menu, or proceed to add the food item to the cart without interruption.

4. The system shall record the customer's food price viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

5. The latest approved pricing information shall remain available for subsequent customer requests until updated by an authorized user.

6. No restaurant, menu, food item, pricing, or promotional data shall be modified during the food price viewing operation.

##### Unsuccessful Completion

1. The requested pricing information shall not be displayed.

2. The system shall notify the customer of the reason the pricing information could not be displayed.

3. The system shall display a platform-defined default message where approved pricing information is unavailable, where applicable.

4. The system shall prevent pricing information associated with unpublished, deleted, disabled, archived, or unauthorized food items from being displayed.

5. No restaurant, menu, food item, pricing, or promotional data shall be modified as a result of the failed food price viewing request.

6. The customer's existing browsing session shall remain active unless termination is required due to security or system policies.

#### 3.3.12.11 Success Response

Upon successful completion of the View Food Price functionality, the system shall:

1. Display the latest approved and customer-visible price associated with the selected food item.

2. Display the current selling price in the platform-supported currency.

3. Display only pricing information associated with active, published, and customer-visible food items.

4. Preserve the approved formatting, currency, and presentation of the pricing information.

5. Display available pricing details, where applicable, including the original price, discount amount, discount percentage, applicable taxes, service charges, final selling price, and other platform-approved pricing information.

6. Clearly distinguish the original price from the discounted selling price, where applicable.

7. Allow the customer to continue browsing the food item details, restaurant menu, or proceed to add the item to the cart without losing the current browsing context.

8. Display the pricing information without modifying any restaurant, menu, food item, pricing, or promotional data.

9. Provide a consistent, accurate, and responsive food price viewing experience across supported devices and platforms.

10. Record food price viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

#### 3.3.12.12 Failure Response

If the View Food Price functionality cannot be completed successfully, the system shall:

1. Inform the customer that the requested pricing information could not be displayed.

2. Display an appropriate and user-friendly message describing the reason for the failure, where applicable.

3. Display a platform-defined default message when approved pricing information is unavailable, where applicable.

4. Prevent the display of pricing information associated with unpublished, deleted, disabled, archived, or unauthorized food items.

5. Allow the customer to retry viewing the pricing information when the failure is temporary.

6. Allow the customer to continue browsing the restaurant menu or food item details if the pricing information cannot be displayed.

7. Record the food price viewing failure event for system monitoring, diagnostics, auditing, and analytics purposes, where applicable.

8. Ensure that no restaurant, menu, food item, pricing, or promotional data is modified as a result of the failed food price viewing request.

9. Maintain the customer's current browsing session and application state unless termination is required due to security or system policies.

### 3.3.13 View Available Customizations

#### 3.3.13.1 Description

The View Available Customizations functionality enables customers to view the customization options available for a selected food item while browsing the restaurant menu. The system shall display the latest approved and customer-visible customization options associated with the selected food item, allowing customers to personalize their orders according to their preferences before adding the item to the cart.

#### 3.3.13.2 Actors

**Primary Actor**

- Customer

**Supporting Actors**

- Menu Service
- Restaurant Service
- Customization Service
- Authentication and Authorization Service (where applicable)

#### 3.3.13.3 Preconditions

1. The customer shall have access to the QuickBite platform.

2. The selected restaurant shall exist and be available for customer access.

3. The selected food item shall exist within the restaurant's latest published menu.

4. The selected food item shall be active and customer-visible.

5. Approved customization options shall be available for the selected food item, where applicable.

6. The customer shall have opened the food item details or restaurant menu before viewing the available customizations.

#### 3.3.13.4 Trigger

The use case begins when the customer selects a food item and requests to view its available customization options from the restaurant menu or food item details page.

#### 3.3.13.5 Input Fields

| Field | Description | Mandatory |
|-------|-------------|-----------|
| Restaurant ID | Unique identifier of the selected restaurant | Yes |
| Food Item ID | Unique identifier of the selected food item | Yes |

#### 3.3.13.6 Business Rules

1. The system shall display only the latest approved and customer-visible customization options associated with the selected food item.

2. Customization options shall be displayed only for active, published, and customer-visible food items.

3. The system shall retrieve customization options only for the selected food item.

4. The displayed customization options shall reflect the latest published version available in the system.

5. Customization options shall be presented in a clear, consistent, and standardized format across the platform.

6. The system shall display only customization options approved for customer selection.

7. Available customization options may include, where applicable:
   - Portion Size
   - Spice Level
   - Cooking Preference
   - Add-ons
   - Extra Toppings
   - Extra Cheese
   - Side Dishes
   - Beverages
   - Sauces and Dips
   - Ingredient Removal
   - Ingredient Replacement
   - Combo Upgrades
   - Other restaurant-defined customization options

8. The system shall clearly identify mandatory and optional customization options, where applicable.

9. The system shall display any additional charges associated with individual customization options, where applicable.

10. The system shall display any minimum or maximum selection limits applicable to customization groups, where configured.

11. If approved customization options are unavailable, the system shall display a platform-defined default message.

12. The system shall not estimate, infer, or generate customization options that have not been approved by the restaurant or platform.

13. Viewing available customizations shall be a read-only operation and shall not modify any restaurant, menu, food item, customization, or pricing data.

14. The system shall record customization viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

15. The system shall comply with applicable business policies, pricing policies, privacy requirements, and regulatory requirements, where applicable.

#### 3.3.13.7 Validations

1. The system shall validate that the selected restaurant exists.

2. The system shall validate that the selected food item exists within the restaurant's latest published menu.

3. The system shall validate that the selected food item is active, published, and customer-visible.

4. The system shall validate that the customization options are associated with the selected food item.

5. The system shall validate that only the latest approved customization options are displayed.

6. The system shall validate that the displayed customization options are approved for customer selection.

7. The system shall validate that all customization options correspond to the latest published version of the selected food item.

8. The system shall validate that any additional charges associated with customization options are correctly configured and approved, where applicable.

9. The system shall validate that mandatory and optional customization options are correctly identified.

10. The system shall validate that configured minimum and maximum selection limits for customization groups are available for display, where applicable.

11. The system shall validate that restricted, unpublished, deleted, disabled, or archived customization options are not displayed to customers.

12. The system shall validate that the customer has permission to access the customization information where authorization policies apply.

13. The system shall validate system availability before retrieving the customization options.

14. The system shall validate that the retrieved customization information is complete and not corrupted before displaying it to the customer.

15. The system shall display a platform-defined default message if approved customization options are unavailable.

16. The system shall validate that the customization viewing request does not modify any restaurant, menu, food item, customization, or pricing data.

#### 3.3.13.8 Main Flow

1. The customer selects a food item from the restaurant menu or food item details page.

2. The customer requests to view the available customization options for the selected food item.

3. The system validates that the selected restaurant exists.

4. The system validates that the selected food item exists within the restaurant's latest published menu.

5. The system validates that the selected food item is active, published, and customer-visible.

6. The system validates that approved customization options are available for the selected food item.

7. The system retrieves the latest approved customization options associated with the selected food item.

8. The system validates that the retrieved customization options are approved for customer selection.

9. The system displays the available customization options in a standardized and customer-friendly format.

10. Where applicable, the system displays customization groups, available options, additional charges, mandatory selections, optional selections, and minimum or maximum selection limits.

11. The customer reviews the available customization options.

12. The system records the customization viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

13. The customer continues browsing the food item details, restaurant menu, or proceeds to customize and add the food item to the cart.

14. The use case ends successfully.

#### 3.3.13.9 Alternate Flows

##### AF-1: Restaurant Does Not Exist

1. The customer attempts to view the available customization options of a food item.
2. The system determines that the selected restaurant does not exist.
3. The system displays an appropriate error message indicating that the restaurant could not be found.
4. The use case ends.

---

##### AF-2: Food Item Does Not Exist

1. The customer selects a food item to view its available customization options.
2. The system determines that the selected food item does not exist in the restaurant's latest published menu.
3. The system displays an appropriate error message.
4. The use case ends.

---

##### AF-3: Approved Customization Options Are Not Available

1. The customer requests to view the available customization options for a food item.
2. The system determines that no approved customer-visible customization options are available for the selected food item.
3. The system displays a platform-defined default message indicating that customization options are currently unavailable.
4. The customer may continue browsing the food item details.
5. The use case continues.

---

##### AF-4: Customization Service Is Unavailable

1. The customer requests to view the available customization options.
2. The system is unable to retrieve the customization information due to a temporary system or service failure.
3. The system displays an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

---

##### AF-5: Customer Is Not Authorized to View the Customization Options

1. The customer requests to view the available customization options of a food item.
2. The system determines that the requested customization information is restricted based on authorization or business policies.
3. The system prevents the customization information from being displayed.
4. The system displays an appropriate authorization message, where applicable.
5. The use case ends.

---

##### AF-6: Customization Information Is Temporarily Unavailable

1. The customer requests to view the available customization options.
2. The system determines that the customization information cannot be retrieved due to a temporary content availability issue.
3. The system displays a platform-defined default message or an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

---

##### AF-7: Food Item Is No Longer Available

1. The customer requests to view the available customization options of a food item.
2. The system determines that the selected food item has become unavailable, unpublished, or disabled.
3. The system prevents the customization information from being displayed.
4. The system informs the customer that the selected food item is no longer available.
5. The use case ends.

#### 3.3.13.10 Postconditions

Upon completion of the View Available Customizations functionality, one of the following postconditions shall apply:

##### Successful Completion

1. The latest approved and customer-visible customization options associated with the selected food item shall be displayed to the customer.

2. The customer shall be able to review all available customization groups, options, additional charges, and selection constraints associated with the selected food item.

3. The customer shall be able to continue browsing the food item details, restaurant menu, or proceed to customize and add the food item to the cart without interruption.

4. The system shall record the customer's customization viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

5. The latest approved customization information shall remain available for subsequent customer requests until updated by an authorized user.

6. No restaurant, menu, food item, customization, pricing, or promotional data shall be modified during the customization viewing operation.

##### Unsuccessful Completion

1. The requested customization information shall not be displayed.

2. The system shall notify the customer of the reason the customization information could not be displayed.

3. The system shall display a platform-defined default message where approved customization information is unavailable, where applicable.

4. The system shall prevent customization information associated with unpublished, deleted, disabled, archived, or unauthorized food items from being displayed.

5. No restaurant, menu, food item, customization, pricing, or promotional data shall be modified as a result of the failed customization viewing request.

6. The customer's existing browsing session shall remain active unless termination is required due to security or system policies.

#### 3.3.13.11 Success Response

Upon successful completion of the View Available Customizations functionality, the system shall:

1. Display the latest approved and customer-visible customization options associated with the selected food item.

2. Display customization groups and their available options in a clear, consistent, and standardized format.

3. Display only customization options associated with active, published, and customer-visible food items.

4. Preserve the approved structure, sequence, and presentation of customization groups and options.

5. Display available customization details, where applicable, including mandatory selections, optional selections, additional charges, minimum selection limits, maximum selection limits, default selections, and other restaurant-approved customization information.

6. Clearly distinguish mandatory customization groups from optional customization groups, where applicable.

7. Clearly display any additional charges applicable to individual customization options.

8. Allow the customer to continue browsing the food item details, restaurant menu, or proceed to customize and add the food item to the cart without losing the current browsing context.

9. Display the customization information without modifying any restaurant, menu, food item, customization, pricing, or promotional data.

10. Provide a consistent, accurate, and responsive customization viewing experience across supported devices and platforms.

11. Record customization viewing activity for analytics, reporting, recommendation, and product improvement purposes, where applicable.

#### 3.3.13.12 Failure Response

If the View Available Customizations functionality cannot be completed successfully, the system shall:

1. Inform the customer that the requested customization information could not be displayed.

2. Display an appropriate and user-friendly message describing the reason for the failure, where applicable.

3. Display a platform-defined default message when approved customization information is unavailable, where applicable.

4. Prevent the display of customization information associated with unpublished, deleted, disabled, archived, or unauthorized food items.

5. Allow the customer to retry viewing the customization information when the failure is temporary.

6. Allow the customer to continue browsing the restaurant menu or food item details if the customization information cannot be displayed.

7. Record the customization viewing failure event for system monitoring, diagnostics, auditing, and analytics purposes, where applicable.

8. Ensure that no restaurant, menu, food item, customization, pricing, or promotional data is modified as a result of the failed customization viewing request.

9. Maintain the customer's current browsing session and application state unless termination is required due to security or system policies.

#### 3.3.13.13 Acceptance Criteria

The View Available Customizations functionality shall be considered successfully implemented when all the following conditions are satisfied:

| AC ID | Acceptance Criteria |
|-------|----------------------|
| AC-VAC-001 | The customer shall be able to view the latest approved customization options associated with a selected food item. |
| AC-VAC-002 | The system shall display only customization options associated with active, published, and customer-visible food items. |
| AC-VAC-003 | The system shall retrieve and display the customization options associated only with the selected food item. |
| AC-VAC-004 | The system shall display all approved customization groups and options in accordance with the platform's content presentation guidelines. |
| AC-VAC-005 | The system shall preserve the approved structure, sequence, and presentation of customization groups and options. |
| AC-VAC-006 | The system shall display available customization details including mandatory selections, optional selections, default selections, additional charges, minimum selection limits, maximum selection limits, and other restaurant-approved customization information, where applicable. |
| AC-VAC-007 | The system shall clearly distinguish mandatory customization groups from optional customization groups, where applicable. |
| AC-VAC-008 | The system shall clearly display any additional charges applicable to customization options, where applicable. |
| AC-VAC-009 | The system shall display a platform-defined default message when approved customization information is unavailable. |
| AC-VAC-010 | The customer shall be able to continue browsing the restaurant menu, food item details, or proceed to customize and add the item to the cart without losing the current browsing context. |
| AC-VAC-011 | The system shall prevent customization information associated with unpublished, deleted, disabled, archived, or unauthorized food items from being displayed. |
| AC-VAC-012 | The system shall ensure that viewing customization information does not modify any restaurant, menu, food item, customization, pricing, or promotional data. |
| AC-VAC-013 | The system shall display an appropriate error message when the customization information cannot be retrieved or displayed. |
| AC-VAC-014 | The system shall record customization viewing activity for analytics and reporting purposes, where applicable. |
| AC-VAC-015 | The system shall provide a consistent, accurate, and responsive customization viewing experience across supported devices and platforms. |


### 3.3.14 Customize Food Item

#### 3.3.14.1 Description

The Customize Food Item functionality enables customers to personalize a selected food item by choosing from the available customization options provided by the restaurant before adding the item to the cart. The system shall allow customers to select, modify, or remove supported customization options while validating business rules, selection limits, pricing impacts, and availability to ensure that the customized food item is eligible for ordering.

#### 3.3.14.2 Actors

**Primary Actor**

- Customer

**Supporting Actors**

- Menu Service
- Restaurant Service
- Customization Service
- Pricing Service
- Cart Service
- Authentication and Authorization Service (where applicable)

#### 3.3.14.3 Preconditions

1. The customer shall have access to the QuickBite platform.

2. The selected restaurant shall exist and be available for customer access.

3. The selected food item shall exist within the restaurant's latest published menu.

4. The selected food item shall be active, published, and available for ordering.

5. Approved customization options shall be available for the selected food item, where applicable.

6. The customer shall have opened the food item customization screen before selecting customization options.

#### 3.3.14.4 Trigger

The use case begins when the customer selects one or more customization options for a food item before adding the item to the cart.

#### 3.3.14.5 Input Fields

| Field | Description | Mandatory |
|-------|-------------|-----------|
| Restaurant ID | Unique identifier of the selected restaurant | Yes |
| Food Item ID | Unique identifier of the selected food item | Yes |
| Customization Group ID | Unique identifier of the customization group | Yes |
| Customization Option ID | Unique identifier of the selected customization option | Yes |
| Quantity | Quantity of the selected customization option, where applicable | No |

#### 3.3.14.6 Business Rules

1. The system shall allow customers to customize only active, published, and customer-orderable food items.

2. The system shall display only the latest approved and customer-selectable customization options associated with the selected food item.

3. Customers shall be permitted to select only customization options belonging to the selected food item.

4. The system shall enforce all mandatory customization groups before allowing the food item to be added to the cart.

5. The system shall enforce the configured minimum and maximum selection limits for each customization group.

6. The system shall allow customers to select one or more customization options where multiple selections are permitted.

7. The system shall prevent duplicate selections when duplicate customization options are not permitted.

8. The system shall automatically recalculate the food item's total price whenever customization selections are added, modified, or removed.

9. Additional charges associated with customization options shall be included in the final food item price.

10. The system shall immediately update the displayed subtotal after every valid customization change.

11. The system shall preserve the customer's selected customization options until the food item is added to the cart, removed, or the customization session expires.

12. The system shall prevent customers from selecting unavailable, inactive, unpublished, deleted, disabled, or restricted customization options.

13. The system shall not permit customization options that violate restaurant-defined business rules or ordering policies.

14. The system shall validate all customization selections before allowing the customized food item to proceed to the Add to Cart operation.

15. Customizing a food item shall not modify the restaurant's master menu, food item definition, pricing configuration, or customization configuration.

16. The system shall record customization activities for analytics, reporting, auditing, recommendation, and product improvement purposes, where applicable.

17. The system shall comply with applicable pricing policies, taxation requirements, food safety regulations, privacy requirements, and other applicable regulatory requirements.

#### 3.3.14.7 Validations

1. The system shall validate that the selected restaurant exists.

2. The system shall validate that the selected food item exists within the restaurant's latest published menu.

3. The system shall validate that the selected food item is active, published, and available for ordering.

4. The system shall validate that the selected customization group belongs to the selected food item.

5. The system shall validate that the selected customization option belongs to the selected customization group.

6. The system shall validate that only approved and customer-selectable customization options are selected.

7. The system shall validate that all mandatory customization groups have been completed before allowing the customized food item to proceed to the Add to Cart operation.

8. The system shall validate that the customer's selections comply with the configured minimum and maximum selection limits for each customization group.

9. The system shall validate that duplicate customization selections are permitted before accepting duplicate selections.

10. The system shall validate that all selected customization options are currently active, available, and eligible for ordering.

11. The system shall validate the additional charges associated with each selected customization option before recalculating the final food item price.

12. The system shall validate that the calculated total price accurately reflects the selected customization options.

13. The system shall validate system availability before processing customization selections.

14. The system shall validate that the customization request does not modify any restaurant, menu, food item, pricing, or customization master data.

15. The system shall display an appropriate validation message whenever one or more customization selections violate the configured business rules or selection constraints.

#### 3.3.14.8 Main Flow

1. The customer selects a food item from the restaurant menu or food item details page.

2. The customer opens the customization screen for the selected food item.

3. The system retrieves the latest approved customization groups and customization options associated with the selected food item.

4. The system displays the available customization groups, customization options, mandatory selections, optional selections, additional charges, and selection limits.

5. The customer selects one or more customization options.

6. The system validates that the selected customization options comply with all configured business rules and selection constraints.

7. The system validates that all mandatory customization groups have been completed.

8. The system recalculates the total price of the customized food item by including all applicable customization charges.

9. The system displays the updated food item price and selected customization summary.

10. The customer reviews the selected customization options and updated pricing.

11. The customer modifies or removes customization selections, where required.

12. The system repeats the validation and price recalculation process for every customization change.

13. The customer confirms the final customization selections.

14. The system stores the selected customization information temporarily for the current ordering session.

15. The customer proceeds to add the customized food item to the cart.

16. The use case ends successfully.

#### 3.3.14.9 Alternate Flows

##### AF-1: Restaurant Does Not Exist

1. The customer attempts to customize a food item.
2. The system determines that the selected restaurant does not exist.
3. The system displays an appropriate error message indicating that the restaurant could not be found.
4. The use case ends.

---

##### AF-2: Food Item Does Not Exist

1. The customer attempts to customize a food item.
2. The system determines that the selected food item does not exist in the restaurant's latest published menu.
3. The system displays an appropriate error message.
4. The use case ends.

---

##### AF-3: Customization Options Are Not Available

1. The customer opens the customization screen for a food item.
2. The system determines that no approved customer-selectable customization options are available for the selected food item.
3. The system displays a platform-defined message indicating that customization is unavailable for the selected food item.
4. The customer may continue ordering the food item without customization, where applicable.
5. The use case continues.

---

##### AF-4: Mandatory Customization Is Not Completed

1. The customer attempts to proceed without selecting all mandatory customization options.
2. The system identifies the missing mandatory customization selections.
3. The system displays an appropriate validation message.
4. The system prevents the customer from proceeding until all mandatory selections are completed.
5. The use case continues.

---

##### AF-5: Selection Limit Is Violated

1. The customer selects more or fewer customization options than permitted for a customization group.
2. The system detects that the configured minimum or maximum selection limit has been violated.
3. The system displays an appropriate validation message.
4. The system prevents the invalid selection from being applied.
5. The use case continues.

---

##### AF-6: Selected Customization Option Is No Longer Available

1. The customer selects a customization option.
2. The system determines that the selected customization option has become unavailable, unpublished, disabled, or deleted.
3. The system prevents the unavailable customization option from being selected.
4. The system informs the customer that the customization option is no longer available.
5. The use case continues.

---

##### AF-7: Price Recalculation Fails

1. The customer modifies one or more customization selections.
2. The system is unable to recalculate the updated food item price due to a temporary processing or service failure.
3. The system displays an appropriate error message.
4. The customer may retry the customization request later.
5. The use case ends.

---

##### AF-8: Customization Service Is Unavailable

1. The customer requests to customize a food item.
2. The system is unable to retrieve or process customization information due to a temporary system or service failure.
3. The system displays an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

---

##### AF-9: Food Item Is No Longer Available

1. The customer attempts to customize a food item.
2. The system determines that the selected food item has become unavailable, unpublished, disabled, or is no longer eligible for ordering.
3. The system prevents further customization.
4. The system informs the customer that the selected food item is no longer available.
5. The use case ends.

#### 3.3.14.10 Postconditions

Upon completion of the Customize Food Item functionality, one of the following postconditions shall apply:

##### Successful Completion

1. The customer's selected customization options shall be successfully associated with the selected food item for the current ordering session.

2. The customized food item shall reflect all validated customization selections, additional charges, and updated pricing.

3. The system shall calculate and display the final customized food item price based on the selected customization options.

4. The customer shall be able to proceed to add the customized food item to the cart or continue modifying the customization selections.

5. The selected customization information shall remain available for the current ordering session until the item is added to the cart, removed, or the session expires.

6. The system shall record the customer's customization activity for analytics, reporting, auditing, recommendation, and product improvement purposes, where applicable.

7. No restaurant, menu, food item, pricing, or customization master data shall be modified during the customization process.

##### Unsuccessful Completion

1. The requested customization selections shall not be applied to the selected food item.

2. The system shall notify the customer of the reason the customization request could not be completed.

3. Invalid or unauthorized customization selections shall be rejected without affecting previously valid selections, where applicable.

4. The system shall prevent the customer from proceeding to the Add to Cart operation until all customization validation requirements are satisfied.

5. No restaurant, menu, food item, pricing, or customization master data shall be modified as a result of the failed customization request.

6. The customer's existing ordering session shall remain active unless termination is required due to security or system policies.

#### 3.3.14.11 Success Response

Upon successful completion of the Customize Food Item functionality, the system shall:

1. Display the customer's selected customization options associated with the selected food item.

2. Display the updated customized food item summary, including all selected customization groups and customization options.

3. Display the recalculated food item price, including applicable customization charges, taxes, service charges, discounts, and the final payable amount, where applicable.

4. Clearly distinguish mandatory and optional customization selections within the customization summary.

5. Display only valid, approved, and customer-selectable customization options associated with the selected food item.

6. Preserve the customer's customization selections throughout the current ordering session until the food item is added to the cart, removed, or the session expires.

7. Allow the customer to modify, replace, or remove customization selections before adding the food item to the cart.

8. Allow the customer to proceed to the Add to Cart functionality with the validated customized food item.

9. Ensure that the customization process does not modify any restaurant, menu, food item, pricing, or customization master data.

10. Provide a consistent, accurate, and responsive food customization experience across supported devices and platforms.

11. Record customization activity for analytics, reporting, auditing, recommendation, and product improvement purposes, where applicable.

#### 3.3.14.12 Failure Response

If the Customize Food Item functionality cannot be completed successfully, the system shall:

1. Inform the customer that the requested food item customization could not be completed.

2. Display an appropriate and user-friendly message describing the reason for the failure, where applicable.

3. Highlight invalid, missing, or conflicting customization selections that require customer action, where applicable.

4. Prevent the customer from proceeding to the Add to Cart functionality until all mandatory customization requirements and validation rules are satisfied.

5. Reject unavailable, unauthorized, unpublished, deleted, disabled, or invalid customization options.

6. Preserve previously valid customization selections where possible, unless they become invalid due to business rules or availability changes.

7. Allow the customer to modify the customization selections and retry the customization request when the failure is recoverable.

8. Record the customization failure event for system monitoring, diagnostics, auditing, and analytics purposes, where applicable.

9. Ensure that no restaurant, menu, food item, pricing, customization master data, or ordering configuration is modified as a result of the failed customization request.

10. Maintain the customer's current ordering session and application state unless termination is required due to security or system policies.

#### 3.3.14.13 Acceptance Criteria

The Customize Food Item functionality shall be considered successfully implemented when all the following conditions are satisfied:

| AC ID | Acceptance Criteria |
|-------|----------------------|
| AC-CFI-001 | The customer shall be able to customize an active, published, and customer-orderable food item. |
| AC-CFI-002 | The system shall display only the latest approved and customer-selectable customization options associated with the selected food item. |
| AC-CFI-003 | The system shall allow customers to select customization options only from the customization groups associated with the selected food item. |
| AC-CFI-004 | The system shall enforce all mandatory customization groups before allowing the customized food item to proceed to the Add to Cart operation. |
| AC-CFI-005 | The system shall enforce the configured minimum and maximum selection limits for each customization group. |
| AC-CFI-006 | The system shall correctly calculate the updated food item price after every valid customization selection, modification, or removal. |
| AC-CFI-007 | The system shall include all applicable customization charges in the final payable amount. |
| AC-CFI-008 | The system shall clearly display the selected customization summary together with the updated pricing information. |
| AC-CFI-009 | The system shall prevent customers from selecting unavailable, unpublished, deleted, disabled, restricted, or invalid customization options. |
| AC-CFI-010 | The system shall preserve valid customization selections throughout the current ordering session until the item is added to the cart, removed, or the session expires. |
| AC-CFI-011 | The customer shall be able to modify, replace, or remove customization selections before adding the food item to the cart. |
| AC-CFI-012 | The system shall prevent the customized food item from proceeding to the Add to Cart operation whenever mandatory customization requirements or validation rules are not satisfied. |
| AC-CFI-013 | The system shall ensure that customizing a food item does not modify any restaurant, menu, food item, pricing, or customization master data. |
| AC-CFI-014 | The system shall display an appropriate validation or error message whenever customization processing cannot be completed successfully. |
| AC-CFI-015 | The system shall record customization activities for analytics, reporting, auditing, and product improvement purposes, where applicable. |
| AC-CFI-016 | The system shall provide a consistent, accurate, and responsive food customization experience across supported devices and platforms. |

### 3.3.15 Select Item Variants

#### 3.3.15.1 Description

The Select Item Variants functionality enables customers to choose an available variant of a selected food item before adding it to the cart. The system shall display the latest approved and customer-selectable item variants, such as size, quantity, flavor, packaging, or other restaurant-defined variants, allowing customers to order the preferred version of the food item while ensuring accurate pricing, availability, and ordering eligibility.

#### 3.3.15.2 Actors

**Primary Actor**

- Customer

**Supporting Actors**

- Menu Service
- Restaurant Service
- Variant Management Service
- Pricing Service
- Cart Service
- Authentication and Authorization Service (where applicable)

#### 3.3.15.3 Preconditions

1. The customer shall have access to the QuickBite platform.

2. The selected restaurant shall exist and be available for customer access.

3. The selected food item shall exist within the restaurant's latest published menu.

4. The selected food item shall be active, published, and available for ordering.

5. Approved item variants shall be available for the selected food item, where applicable.

6. The customer shall have opened the food item details or variant selection screen before selecting an item variant.

#### 3.3.15.4 Trigger

The use case begins when the customer selects a variant of a food item from the available item variants before adding the food item to the cart.

#### 3.3.15.5 Input Fields

| Field | Description | Mandatory |
|-------|-------------|-----------|
| Restaurant ID | Unique identifier of the selected restaurant | Yes |
| Food Item ID | Unique identifier of the selected food item | Yes |
| Variant ID | Unique identifier of the selected item variant | Yes |
| Variant Option ID | Unique identifier of the selected variant option | Yes |

#### 3.3.15.6 Business Rules

1. The system shall display only the latest approved and customer-selectable variants associated with the selected food item.

2. Item variants shall be displayed only for active, published, and customer-orderable food items.

3. The system shall retrieve item variants only for the selected food item.

4. The displayed item variants shall reflect the latest published version available in the system.

5. Item variants may include, where applicable:
   - Size
   - Quantity
   - Weight
   - Flavor
   - Packaging Type
   - Portion
   - Meal Type
   - Beverage Size
   - Combo Variant
   - Other restaurant-defined variants

6. The system shall display only item variants approved for customer selection.

7. Only one variant option shall be selectable within a single variant group unless the restaurant configuration explicitly allows multiple selections.

8. The system shall automatically update the food item price whenever the customer selects a different variant.

9. The displayed price shall reflect the selected variant together with any applicable pricing adjustments.

10. The system shall prevent customers from selecting unavailable, unpublished, deleted, disabled, inactive, or restricted variants.

11. The system shall preserve the customer's selected variant throughout the current ordering session until the food item is added to the cart, removed, or the session expires.

12. If no approved variants are available, the system shall display a platform-defined default message indicating that no variants are currently available.

13. Selecting an item variant shall be a transactional ordering operation and shall not modify any restaurant, menu, food item, pricing, or variant master data.

14. The system shall record item variant selection activity for analytics, reporting, auditing, recommendation, and product improvement purposes, where applicable.

15. The system shall comply with applicable pricing policies, taxation requirements, privacy requirements, and other applicable regulatory requirements.

#### 3.3.15.7 Validations

1. The system shall validate that the selected restaurant exists.

2. The system shall validate that the selected food item exists within the restaurant's latest published menu.

3. The system shall validate that the selected food item is active, published, and available for ordering.

4. The system shall validate that the selected variant group belongs to the selected food item.

5. The system shall validate that the selected variant option belongs to the selected variant group.

6. The system shall validate that only approved and customer-selectable variants are available for selection.

7. The system shall validate that the selected variant is active, available, and eligible for ordering.

8. The system shall validate that only one variant option is selected within a variant group unless multiple selections are explicitly permitted.

9. The system shall validate that the displayed food item price accurately reflects the selected variant and all applicable pricing adjustments.

10. The system shall validate that restricted, unpublished, deleted, disabled, inactive, or archived variants are not available for customer selection.

11. The system shall validate system availability before retrieving or processing item variant information.

12. The system shall validate that the retrieved variant information is complete and not corrupted before displaying it to the customer.

13. The system shall display a platform-defined default message if approved item variants are unavailable.

14. The system shall validate that selecting an item variant does not modify any restaurant, menu, food item, pricing, or variant master data.

15. The system shall display an appropriate validation message whenever the selected variant violates configured business rules or ordering constraints.

#### 3.3.15.8 Main Flow

1. The customer selects a food item from the restaurant menu or food item details page.

2. The customer opens the item variant selection screen for the selected food item.

3. The system retrieves the latest approved item variants associated with the selected food item.

4. The system displays the available variant groups, variant options, applicable pricing adjustments, availability status, and other variant information.

5. The customer selects the preferred item variant.

6. The system validates that the selected variant is active, approved, customer-selectable, and available for ordering.

7. The system validates that the selected variant complies with the configured variant selection rules.

8. The system recalculates the food item's price based on the selected variant and any applicable pricing adjustments.

9. The system displays the updated food item price together with the selected variant summary.

10. The customer reviews the selected variant and updated pricing.

11. The customer changes the selected variant, where required.

12. The system repeats the validation and price recalculation process for every variant change.

13. The customer confirms the final item variant selection.

14. The system stores the selected variant information temporarily for the current ordering session.

15. The customer proceeds to add the selected food item variant to the cart.

16. The use case ends successfully.

#### 3.3.15.9 Alternate Flows

##### AF-1: Restaurant Does Not Exist

1. The customer attempts to select an item variant.
2. The system determines that the selected restaurant does not exist.
3. The system displays an appropriate error message indicating that the restaurant could not be found.
4. The use case ends.

---

##### AF-2: Food Item Does Not Exist

1. The customer attempts to select an item variant for a food item.
2. The system determines that the selected food item does not exist in the restaurant's latest published menu.
3. The system displays an appropriate error message.
4. The use case ends.

---

##### AF-3: Approved Item Variants Are Not Available

1. The customer opens the item variant selection screen.
2. The system determines that no approved customer-selectable item variants are available for the selected food item.
3. The system displays a platform-defined message indicating that item variants are currently unavailable.
4. The customer may continue ordering the default food item, where applicable.
5. The use case continues.

---

##### AF-4: Selected Variant Is No Longer Available

1. The customer selects an item variant.
2. The system determines that the selected variant has become unavailable, unpublished, disabled, deleted, or inactive.
3. The system prevents the unavailable variant from being selected.
4. The system informs the customer that the selected variant is no longer available.
5. The use case continues.

---

##### AF-5: Invalid Variant Selection

1. The customer selects a variant that violates the configured variant selection rules.
2. The system detects the invalid variant selection.
3. The system displays an appropriate validation message.
4. The system prevents the invalid variant from being selected.
5. The use case continues.

---

##### AF-6: Price Recalculation Fails

1. The customer changes the selected item variant.
2. The system is unable to recalculate the updated food item price due to a temporary processing or service failure.
3. The system displays an appropriate error message.
4. The customer may retry the variant selection later.
5. The use case ends.

---

##### AF-7: Variant Management Service Is Unavailable

1. The customer requests to select an item variant.
2. The system is unable to retrieve or process the item variant information due to a temporary system or service failure.
3. The system displays an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

---

##### AF-8: Food Item Is No Longer Available

1. The customer attempts to select an item variant.
2. The system determines that the selected food item has become unavailable, unpublished, disabled, or is no longer eligible for ordering.
3. The system prevents further variant selection.
4. The system informs the customer that the selected food item is no longer available.
5. The use case ends.

#### 3.3.15.10 Postconditions

Upon completion of the Select Item Variants functionality, one of the following postconditions shall apply:

##### Successful Completion

1. The customer's selected item variant shall be successfully associated with the selected food item for the current ordering session.

2. The selected food item shall reflect the validated variant selection together with the corresponding pricing adjustments.

3. The system shall calculate and display the updated food item price based on the selected variant.

4. The customer shall be able to proceed to add the selected food item variant to the cart or continue modifying the variant selection.

5. The selected variant information shall remain available for the current ordering session until the food item is added to the cart, removed, or the session expires.

6. The system shall record the customer's item variant selection activity for analytics, reporting, auditing, recommendation, and product improvement purposes, where applicable.

7. No restaurant, menu, food item, pricing, or variant master data shall be modified during the item variant selection process.

##### Unsuccessful Completion

1. The requested item variant selection shall not be applied to the selected food item.

2. The system shall notify the customer of the reason the item variant selection could not be completed.

3. Invalid or unauthorized variant selections shall be rejected without affecting previously valid selections, where applicable.

4. The system shall prevent the customer from proceeding to the Add to Cart operation until all variant validation requirements are satisfied.

5. No restaurant, menu, food item, pricing, or variant master data shall be modified as a result of the failed item variant selection request.

6. The customer's existing ordering session shall remain active unless termination is required due to security or system policies.

#### 3.3.15.11 Success Response

Upon successful completion of the Select Item Variants functionality, the system shall:

1. Display the customer's selected item variant associated with the selected food item.

2. Display the updated food item summary, including the selected variant and its applicable attributes.

3. Display the recalculated food item price, including any applicable variant-based pricing adjustments, taxes, service charges, discounts, and the final payable amount, where applicable.

4. Clearly indicate the currently selected variant within each variant group.

5. Display only valid, approved, and customer-selectable variants associated with the selected food item.

6. Preserve the customer's selected item variant throughout the current ordering session until the food item is added to the cart, removed, or the session expires.

7. Allow the customer to change the selected variant before adding the food item to the cart.

8. Allow the customer to proceed to the Add to Cart functionality with the validated selected item variant.

9. Ensure that selecting an item variant does not modify any restaurant, menu, food item, pricing, or variant master data.

10. Provide a consistent, accurate, and responsive item variant selection experience across supported devices and platforms.

11. Record item variant selection activity for analytics, reporting, auditing, recommendation, and product improvement purposes, where applicable.

#### 3.3.15.12 Failure Response

If the Select Item Variants functionality cannot be completed successfully, the system shall:

1. Inform the customer that the requested item variant selection could not be completed.

2. Display an appropriate and user-friendly message describing the reason for the failure, where applicable.

3. Highlight invalid, unavailable, or conflicting variant selections that require customer action, where applicable.

4. Prevent the customer from proceeding to the Add to Cart functionality until all variant validation requirements and business rules are satisfied.

5. Reject unavailable, unauthorized, unpublished, deleted, disabled, inactive, or invalid item variants.

6. Preserve previously valid item variant selections where possible, unless they become invalid due to business rules or availability changes.

7. Allow the customer to modify the selected item variant and retry the request when the failure is recoverable.

8. Record the item variant selection failure event for system monitoring, diagnostics, auditing, and analytics purposes, where applicable.

9. Ensure that no restaurant, menu, food item, pricing, variant master data, or ordering configuration is modified as a result of the failed item variant selection request.

10. Maintain the customer's current ordering session and application state unless termination is required due to security or system policies.

#### 3.3.15.13 Acceptance Criteria

The Select Item Variants functionality shall be considered successfully implemented when all the following conditions are satisfied:

| AC ID | Acceptance Criteria |
|-------|----------------------|
| AC-SIV-001 | The customer shall be able to select an approved item variant associated with a selected food item. |
| AC-SIV-002 | The system shall display only item variants associated with active, published, and customer-orderable food items. |
| AC-SIV-003 | The system shall retrieve and display only the approved item variants associated with the selected food item. |
| AC-SIV-004 | The system shall display all approved variant groups and variant options in accordance with the platform's content presentation guidelines. |
| AC-SIV-005 | The system shall preserve the approved structure, sequence, and presentation of item variants. |
| AC-SIV-006 | The system shall allow the customer to select only valid and customer-selectable variant options. |
| AC-SIV-007 | The system shall ensure that only one variant option can be selected within a variant group unless multiple selections are explicitly permitted. |
| AC-SIV-008 | The system shall automatically recalculate the food item price whenever the selected variant changes. |
| AC-SIV-009 | The system shall display the updated pricing information, including all applicable variant-based pricing adjustments. |
| AC-SIV-010 | The system shall prevent customers from selecting unavailable, unpublished, deleted, disabled, inactive, restricted, or invalid item variants. |
| AC-SIV-011 | The system shall preserve the selected item variant throughout the current ordering session until the item is added to the cart, removed, or the session expires. |
| AC-SIV-012 | The customer shall be able to modify the selected item variant before adding the food item to the cart. |
| AC-SIV-013 | The system shall ensure that selecting an item variant does not modify any restaurant, menu, food item, pricing, or variant master data. |
| AC-SIV-014 | The system shall display an appropriate validation or error message whenever the item variant selection cannot be completed successfully. |
| AC-SIV-015 | The system shall record item variant selection activities for analytics, reporting, auditing, and product improvement purposes, where applicable. |
| AC-SIV-016 | The system shall provide a consistent, accurate, and responsive item variant selection experience across supported devices and platforms. |

### 3.3.16 Add Extra Toppings

#### 3.3.16.1 Description

This use case allows the customer to add optional extra toppings to a selected food item before adding it to the cart. The system shall display only approved, active, and applicable toppings configured for the selected food item. The customer may select one or more toppings, subject to restaurant-defined limits and business rules. The system shall validate the selected toppings, recalculate the food item's price, and associate the selected toppings with the food item for the current ordering session without modifying any master data.

#### 3.3.16.2 Actors

**Primary Actor:**
- Customer

**Supporting Actors:**
- Menu Service
- Restaurant Service
- Toppings Management Service
- Pricing Service
- Cart Service
- Authentication and Authorization Service (where applicable)

#### 3.3.16.3 Preconditions

1. The customer shall have access to the QuickBite platform.

2. The selected restaurant shall exist and be available for ordering.

3. The selected food item shall exist within the restaurant's latest published menu.

4. The selected food item shall be active, published, and available for ordering.

5. The selected food item shall support extra toppings.

6. Approved and customer-selectable toppings shall be configured for the selected food item.

7. The customer shall have opened the Add Extra Toppings screen for the selected food item.

8. Required restaurant, menu, pricing, and topping information shall be successfully retrieved by the system.

9. The system and all required supporting services shall be operational and available.

10. The customer's ordering session shall be active.

#### 3.3.16.4 Trigger

The use case is triggered when the customer selects the option to add extra toppings for a selected food item before adding the item to the cart.

#### 3.3.16.5 Input Fields

| Field | Description | Mandatory |
|-------|-------------|-----------|
| Restaurant ID | Unique identifier of the selected restaurant | Yes |
| Food Item ID | Unique identifier of the selected food item | Yes |
| Topping ID | Unique identifier of the topping group | Yes |
| Topping Option ID | Unique identifier of the selected topping option | Yes |
| Quantity | Number of units for the selected topping, where supported | No |

#### 3.3.16.6 Business Rules

1. The system shall display only the latest approved extra toppings configured for the selected food item.

2. The system shall display extra toppings only for food items that are active, published, and available for ordering.

3. The system shall retrieve extra toppings only for the selected food item.

4. The system shall display only approved, active, and customer-selectable extra toppings.

5. Extra toppings may include, but are not limited to:
   - Extra Cheese
   - Paneer
   - Chicken
   - Bacon
   - Mushrooms
   - Olives
   - Jalapeños
   - Sweet Corn
   - Onions
   - Tomatoes
   - Capsicum
   - Pepperoni
   - Sausages
   - Herbs and Seasonings
   - Sauce Add-ons
   - Other restaurant-defined toppings

6. The system shall display the additional price associated with each extra topping, where applicable.

7. The system shall allow customers to select one or more extra toppings in accordance with restaurant-defined configuration.

8. The system shall enforce the minimum and maximum topping selection limits configured for the selected food item.

9. The system shall validate the availability of every selected topping before confirming the selection.

10. The system shall automatically recalculate the food item's price whenever extra toppings are added, removed, or modified.

11. The recalculated price shall include all applicable topping charges, taxes, service charges, discounts, and pricing rules.

12. The system shall prevent customers from selecting unavailable, unpublished, disabled, deleted, inactive, or restricted extra toppings.

13. The selected extra toppings shall remain associated with the food item throughout the current ordering session until the item is added to the cart, removed, or the session expires.

14. Adding extra toppings shall not modify any restaurant, menu, food item, pricing, topping, or configuration master data.

15. The system shall record extra topping selection activities for analytics, reporting, auditing, recommendation, and product improvement purposes, where applicable.

16. The system shall comply with applicable pricing, taxation, food safety, privacy, accessibility, and regulatory requirements.

#### 3.3.16.7 Validations

1. The system shall validate that the selected restaurant exists.

2. The system shall validate that the selected food item exists within the restaurant's latest published menu.

3. The system shall validate that the selected food item is active, published, and available for ordering.

4. The system shall validate that the selected food item supports extra toppings.

5. The system shall validate that the selected topping group belongs to the selected food item.

6. The system shall validate that the selected topping option belongs to the selected topping group.

7. The system shall validate that only approved and customer-selectable extra toppings are available for selection.

8. The system shall validate that each selected topping is active, available, and eligible for ordering.

9. The system shall validate that the customer's topping selection complies with the configured minimum and maximum topping selection limits.

10. The system shall validate the quantity specified for each topping, where quantity-based topping selection is supported.

11. The system shall validate that the displayed food item price accurately reflects all selected extra toppings and applicable pricing adjustments.

12. The system shall validate that unavailable, unpublished, deleted, disabled, inactive, archived, or restricted extra toppings cannot be selected.

13. The system shall validate system availability before retrieving or processing extra topping information.

14. The system shall validate that the retrieved extra topping information is complete and not corrupted before displaying it to the customer.

15. The system shall display a platform-defined default message if approved extra toppings are unavailable for the selected food item.

16. The system shall validate that adding extra toppings does not modify any restaurant, menu, food item, pricing, topping, or configuration master data.

17. The system shall display an appropriate validation message whenever the selected extra toppings violate configured business rules or ordering constraints.

#### 3.3.16.8 Main Flow

1. The customer selects a food item from the restaurant menu or food item details page.

2. The customer opens the Add Extra Toppings screen for the selected food item.

3. The system retrieves the latest approved extra toppings configured for the selected food item.

4. The system displays the available topping groups, topping options, applicable prices, availability status, quantity options (where supported), and other topping information.

5. The customer selects one or more extra toppings.

6. The customer specifies the quantity for each selected topping, where quantity-based topping selection is supported.

7. The system validates that each selected topping is active, approved, customer-selectable, and available for ordering.

8. The system validates that the customer's topping selection complies with the configured minimum and maximum topping selection limits.

9. The system recalculates the food item's price based on the selected extra toppings and all applicable pricing adjustments.

10. The system displays the updated food item price together with the selected topping summary.

11. The customer reviews the selected extra toppings and updated pricing.

12. The customer adds, removes, or modifies the selected extra toppings, where required.

13. The system repeats the validation and price recalculation process for every topping modification.

14. The customer confirms the final extra topping selection.

15. The system stores the selected extra toppings temporarily for the current ordering session.

16. The customer proceeds to add the customized food item to the cart.

17. The use case ends successfully.

#### 3.3.16.9 Alternate Flows

##### AF-1: Restaurant Does Not Exist

1. The customer attempts to add extra toppings.
2. The system determines that the selected restaurant does not exist.
3. The system displays an appropriate error message indicating that the restaurant could not be found.
4. The use case ends.

---

##### AF-2: Food Item Does Not Exist

1. The customer attempts to add extra toppings to a food item.
2. The system determines that the selected food item does not exist in the restaurant's latest published menu.
3. The system displays an appropriate error message.
4. The use case ends.

---

##### AF-3: Extra Toppings Are Not Available

1. The customer opens the Add Extra Toppings screen.
2. The system determines that no approved customer-selectable extra toppings are configured for the selected food item.
3. The system displays a platform-defined message indicating that extra toppings are currently unavailable.
4. The customer may continue ordering the food item without extra toppings.
5. The use case continues.

---

##### AF-4: Selected Topping Is No Longer Available

1. The customer selects one or more extra toppings.
2. The system determines that one or more selected toppings have become unavailable, unpublished, disabled, deleted, or inactive.
3. The system prevents the unavailable topping from being selected.
4. The system informs the customer that the selected topping is no longer available.
5. The use case continues.

---

##### AF-5: Topping Selection Limit Exceeded

1. The customer selects extra toppings exceeding the configured maximum limit.
2. The system detects that the topping selection violates the configured business rules.
3. The system displays an appropriate validation message.
4. The system prevents the customer from confirming the invalid topping selection.
5. The use case continues.

---

##### AF-6: Invalid Topping Quantity

1. The customer specifies an invalid quantity for a selected topping.
2. The system detects that the specified quantity violates the configured quantity constraints.
3. The system displays an appropriate validation message.
4. The system requests the customer to provide a valid quantity.
5. The use case continues.

---

##### AF-7: Price Recalculation Fails

1. The customer adds, removes, or modifies extra toppings.
2. The system is unable to recalculate the updated food item price due to a temporary processing or service failure.
3. The system displays an appropriate error message.
4. The customer may retry the topping selection later.
5. The use case ends.

---

##### AF-8: Toppings Management Service Is Unavailable

1. The customer requests to add extra toppings.
2. The system is unable to retrieve or process topping information due to a temporary system or service failure.
3. The system displays an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

---

##### AF-9: Food Item Is No Longer Available

1. The customer attempts to add extra toppings.
2. The system determines that the selected food item has become unavailable, unpublished, disabled, or is no longer eligible for ordering.
3. The system prevents further topping selection.
4. The system informs the customer that the selected food item is no longer available.
5. The use case ends.

#### 3.3.16.10 Postconditions

Upon completion of the Add Extra Toppings functionality, one of the following postconditions shall apply:

##### Successful Completion

1. The selected extra toppings shall be successfully associated with the selected food item for the current ordering session.

2. The selected food item shall reflect all validated extra topping selections together with the corresponding pricing adjustments.

3. The system shall calculate and display the updated food item price based on the selected extra toppings.

4. The customer shall be able to proceed to add the customized food item to the cart or continue modifying the topping selection.

5. The selected extra toppings shall remain associated with the food item throughout the current ordering session until the food item is added to the cart, removed, or the session expires.

6. The system shall record extra topping selection activities for analytics, reporting, auditing, recommendation, and product improvement purposes, where applicable.

7. No restaurant, menu, food item, pricing, topping, or configuration master data shall be modified during the extra topping selection process.

##### Unsuccessful Completion

1. The requested extra topping selection shall not be applied to the selected food item.

2. The system shall notify the customer of the reason the extra topping selection could not be completed.

3. Invalid or unauthorized topping selections shall be rejected without affecting previously valid selections, where applicable.

4. The system shall prevent the customer from proceeding to the Add to Cart operation until all topping validation requirements are satisfied.

5. No restaurant, menu, food item, pricing, topping, or configuration master data shall be modified as a result of the failed extra topping selection request.

6. The customer's existing ordering session shall remain active unless termination is required due to security or system policies.

#### 3.3.16.11 Success Response

Upon successful completion of the Add Extra Toppings functionality, the system shall:

1. Display the selected extra toppings associated with the selected food item.

2. Display the updated food item summary, including all selected extra toppings and their applicable attributes.

3. Display the recalculated food item price, including all applicable topping charges, taxes, service charges, discounts, and the final payable amount, where applicable.

4. Clearly indicate the currently selected extra toppings within each topping group.

5. Display only valid, approved, active, and customer-selectable extra toppings associated with the selected food item.

6. Preserve the selected extra toppings throughout the current ordering session until the food item is added to the cart, removed, or the session expires.

7. Allow the customer to add, remove, or modify extra toppings before adding the food item to the cart.

8. Allow the customer to proceed to the Add to Cart functionality with the validated extra topping selection.

9. Ensure that adding extra toppings does not modify any restaurant, menu, food item, pricing, topping, or configuration master data.

10. Provide a consistent, accurate, and responsive extra topping selection experience across supported devices and platforms.

11. Record extra topping selection activities for analytics, reporting, auditing, recommendation, and product improvement purposes, where applicable.

#### 3.3.16.12 Failure Response

If the Add Extra Toppings functionality cannot be completed successfully, the system shall:

1. Inform the customer that the requested extra topping selection could not be completed.

2. Display an appropriate and user-friendly message describing the reason for the failure, where applicable.

3. Highlight invalid, unavailable, or conflicting topping selections that require customer action, where applicable.

4. Prevent the customer from proceeding to the Add to Cart functionality until all topping validation requirements and business rules are satisfied.

5. Reject unavailable, unauthorized, unpublished, deleted, disabled, inactive, restricted, or invalid extra toppings.

6. Preserve previously valid extra topping selections where possible, unless they become invalid due to business rules or availability changes.

7. Allow the customer to modify the selected extra toppings and retry the request when the failure is recoverable.

8. Record the extra topping selection failure event for system monitoring, diagnostics, auditing, and analytics purposes, where applicable.

9. Ensure that no restaurant, menu, food item, pricing, topping, or configuration master data is modified as a result of the failed extra topping selection request.

10. Maintain the customer's current ordering session and application state unless termination is required due to security or system policies.

#### 3.3.16.13 Acceptance Criteria

The Add Extra Toppings functionality shall be considered successfully implemented when all the following conditions are satisfied:

| AC ID | Acceptance Criteria |
|-------|----------------------|
| AC-AET-001 | The customer shall be able to add approved extra toppings associated with the selected food item. |
| AC-AET-002 | The system shall display extra toppings only for food items that are active, published, and available for ordering. |
| AC-AET-003 | The system shall retrieve and display only approved, active, and customer-selectable extra toppings configured for the selected food item. |
| AC-AET-004 | The system shall display all topping groups, topping options, applicable prices, and availability information in accordance with the platform's presentation guidelines. |
| AC-AET-005 | The system shall allow customers to select one or more extra toppings based on the restaurant's configuration. |
| AC-AET-006 | The system shall enforce the configured minimum and maximum topping selection limits for the selected food item. |
| AC-AET-007 | The system shall validate that every selected topping is active, approved, customer-selectable, and available for ordering. |
| AC-AET-008 | The system shall automatically recalculate the food item price whenever extra toppings are added, removed, or modified. |
| AC-AET-009 | The system shall display the updated pricing information, including all applicable topping charges and pricing adjustments. |
| AC-AET-010 | The system shall prevent customers from selecting unavailable, unpublished, deleted, disabled, inactive, restricted, or invalid extra toppings. |
| AC-AET-011 | The system shall preserve the selected extra toppings throughout the current ordering session until the food item is added to the cart, removed, or the session expires. |
| AC-AET-012 | The customer shall be able to modify or remove selected extra toppings before adding the food item to the cart. |
| AC-AET-013 | The system shall ensure that adding extra toppings does not modify any restaurant, menu, food item, pricing, topping, or configuration master data. |
| AC-AET-014 | The system shall display an appropriate validation or error message whenever extra topping selection cannot be completed successfully. |
| AC-AET-015 | The system shall record extra topping selection activities for analytics, reporting, auditing, and product improvement purposes, where applicable. |
| AC-AET-016 | The system shall provide a consistent, accurate, and responsive extra topping selection experience across supported devices and platforms. |

### 3.3.17 Remove Ingredients

#### 3.3.17.1 Description

This use case allows the customer to remove eligible ingredients from a selected food item before adding it to the cart. The system shall display only ingredients that are approved for customer removal based on the restaurant's configuration. The customer may remove one or more removable ingredients, subject to applicable business rules. The system shall validate the requested ingredient removals, update the food item customization summary, recalculate the price where applicable, and associate the customized ingredient selection with the food item for the current ordering session without modifying any master data.

#### 3.3.17.2 Actors

**Primary Actor:**
- Customer

**Supporting Actors:**
- Menu Service
- Restaurant Service
- Ingredient Management Service
- Pricing Service
- Cart Service
- Authentication and Authorization Service (where applicable)

#### 3.3.17.3 Preconditions

1. The customer shall have access to the QuickBite platform.

2. The selected restaurant shall exist and be available for ordering.

3. The selected food item shall exist within the restaurant's latest published menu.

4. The selected food item shall be active, published, and available for ordering.

5. The selected food item shall support ingredient customization through ingredient removal.

6. One or more ingredients shall be configured as customer-removable for the selected food item.

7. The customer shall have opened the Remove Ingredients screen for the selected food item.

8. Required restaurant, menu, ingredient, pricing, and customization information shall be successfully retrieved by the system.

9. The system and all required supporting services shall be operational and available.

10. The customer's ordering session shall be active.

#### 3.3.17.4 Trigger

The use case is triggered when the customer selects the option to remove one or more eligible ingredients from a selected food item before adding the item to the cart.

#### 3.3.17.5 Input Fields

| Field | Description | Mandatory |
|-------|-------------|-----------|
| Restaurant ID | Unique identifier of the selected restaurant | Yes |
| Food Item ID | Unique identifier of the selected food item | Yes |
| Ingredient ID | Unique identifier of the removable ingredient | Yes |
| Remove Ingredient | Indicates whether the selected ingredient should be removed from the food item | Yes |

#### 3.3.17.6 Business Rules

1. The system shall display only the latest approved removable ingredients configured for the selected food item.

2. The system shall display removable ingredients only for food items that are active, published, and available for ordering.

3. The system shall retrieve removable ingredients only for the selected food item.

4. The system shall display only ingredients that are approved and configured by the restaurant as customer-removable.

5. Ingredients that are mandatory, fixed, or non-removable for recipe consistency, food safety, legal compliance, or operational reasons shall not be available for removal.

6. The customer may remove one or more eligible ingredients in accordance with the restaurant's customization configuration.

7. The system shall validate every requested ingredient removal before applying the customization.

8. The system shall update the food item customization summary immediately after each valid ingredient removal.

9. The system shall automatically recalculate the food item's price whenever ingredient removal affects pricing, where applicable.

10. The recalculated price shall include all applicable pricing rules, taxes, service charges, discounts, and restaurant-specific pricing policies.

11. The system shall prevent customers from removing unavailable, unpublished, deleted, disabled, inactive, restricted, or non-removable ingredients.

12. The selected ingredient removal preferences shall remain associated with the food item throughout the current ordering session until the item is added to the cart, removed, or the session expires.

13. Removing ingredients shall not modify any restaurant, menu, food item, ingredient, pricing, recipe, or configuration master data.

14. The system shall record ingredient removal activities for analytics, reporting, auditing, recommendation, and product improvement purposes, where applicable.

15. The system shall comply with applicable food safety, allergen disclosure, pricing, taxation, privacy, accessibility, and regulatory requirements.

#### 3.3.17.7 Validations

1. The system shall validate that the selected restaurant exists.

2. The system shall validate that the selected food item exists within the restaurant's latest published menu.

3. The system shall validate that the selected food item is active, published, and available for ordering.

4. The system shall validate that the selected food item supports ingredient removal customization.

5. The system shall validate that the selected ingredient belongs to the selected food item.

6. The system shall validate that the selected ingredient is configured as customer-removable.

7. The system shall validate that only approved, active, and customer-removable ingredients are available for removal.

8. The system shall validate that the requested ingredient removal complies with all restaurant-defined customization rules.

9. The system shall validate that mandatory, fixed, restricted, or non-removable ingredients cannot be removed.

10. The system shall validate that the displayed food item price accurately reflects all approved ingredient removal pricing adjustments, where applicable.

11. The system shall validate that unavailable, unpublished, deleted, disabled, inactive, archived, or restricted ingredients cannot be selected for removal.

12. The system shall validate system availability before retrieving or processing ingredient customization information.

13. The system shall validate that the retrieved ingredient information is complete and not corrupted before displaying it to the customer.

14. The system shall display a platform-defined default message if no removable ingredients are available for the selected food item.

15. The system shall validate that removing ingredients does not modify any restaurant, menu, food item, ingredient, pricing, recipe, or configuration master data.

16. The system shall display an appropriate validation message whenever the requested ingredient removal violates configured business rules or ordering constraints.

#### 3.3.17.8 Main Flow

1. The customer selects a food item from the restaurant menu or food item details page.

2. The customer opens the Remove Ingredients screen for the selected food item.

3. The system retrieves the latest approved customer-removable ingredients configured for the selected food item.

4. The system displays the list of removable ingredients together with their current selection status and any applicable customization information.

5. The customer selects one or more ingredients to remove from the food item.

6. The system validates that each selected ingredient is approved, customer-removable, active, and eligible for removal.

7. The system validates that the requested ingredient removal complies with all configured customization rules and business constraints.

8. The system updates the food item customization summary to reflect the selected ingredient removals.

9. The system recalculates the food item's price where ingredient removal affects pricing.

10. The system displays the updated food item price together with the revised customization summary.

11. The customer reviews the selected ingredient removals and updated pricing.

12. The customer adds, restores, or modifies ingredient removal selections, where required.

13. The system repeats the validation and price recalculation process for every ingredient customization change.

14. The customer confirms the final ingredient removal selection.

15. The system stores the selected ingredient removal preferences temporarily for the current ordering session.

16. The customer proceeds to add the customized food item to the cart.

17. The use case ends successfully.

#### 3.3.17.9 Alternate Flows

##### AF-1: Restaurant Does Not Exist

1. The customer attempts to remove one or more ingredients.
2. The system determines that the selected restaurant does not exist.
3. The system displays an appropriate error message indicating that the restaurant could not be found.
4. The use case ends.

---

##### AF-2: Food Item Does Not Exist

1. The customer attempts to remove ingredients from a food item.
2. The system determines that the selected food item does not exist in the restaurant's latest published menu.
3. The system displays an appropriate error message.
4. The use case ends.

---

##### AF-3: No Removable Ingredients Are Available

1. The customer opens the Remove Ingredients screen.
2. The system determines that no customer-removable ingredients are configured for the selected food item.
3. The system displays a platform-defined message indicating that ingredient removal is not available for the selected food item.
4. The customer may continue ordering the food item without customization.
5. The use case continues.

---

##### AF-4: Selected Ingredient Cannot Be Removed

1. The customer attempts to remove an ingredient.
2. The system determines that the selected ingredient is mandatory, fixed, restricted, inactive, or otherwise non-removable.
3. The system prevents the ingredient from being removed.
4. The system displays an appropriate validation message.
5. The use case continues.

---

##### AF-5: Ingredient Is No Longer Available

1. The customer requests to remove an ingredient.
2. The system determines that the ingredient has become unavailable, unpublished, deleted, disabled, or inactive.
3. The system prevents the requested customization.
4. The system informs the customer that the selected ingredient is no longer available for customization.
5. The use case continues.

---

##### AF-6: Price Recalculation Fails

1. The customer removes or restores one or more ingredients.
2. The system is unable to recalculate the updated food item price due to a temporary processing or service failure.
3. The system displays an appropriate error message.
4. The customer may retry the customization later.
5. The use case ends.

---

##### AF-7: Ingredient Management Service Is Unavailable

1. The customer requests to remove ingredients.
2. The system is unable to retrieve or process ingredient customization information due to a temporary system or service failure.
3. The system displays an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

---

##### AF-8: Food Item Is No Longer Available

1. The customer attempts to remove ingredients.
2. The system determines that the selected food item has become unavailable, unpublished, disabled, or is no longer eligible for ordering.
3. The system prevents further ingredient customization.
4. The system informs the customer that the selected food item is no longer available.
5. The use case ends.

#### 3.3.17.10 Postconditions

Upon completion of the Remove Ingredients functionality, one of the following postconditions shall apply:

##### Successful Completion

1. The selected ingredient removal preferences shall be successfully associated with the selected food item for the current ordering session.

2. The selected food item shall reflect all validated ingredient removal customizations together with any applicable pricing adjustments.

3. The system shall calculate and display the updated food item price where ingredient removal affects pricing.

4. The customer shall be able to proceed to add the customized food item to the cart or continue modifying the ingredient removal selections.

5. The selected ingredient removal preferences shall remain associated with the food item throughout the current ordering session until the food item is added to the cart, removed, or the session expires.

6. The system shall record ingredient removal activities for analytics, reporting, auditing, recommendation, and product improvement purposes, where applicable.

7. No restaurant, menu, food item, ingredient, pricing, recipe, or configuration master data shall be modified during the ingredient removal customization process.

##### Unsuccessful Completion

1. The requested ingredient removal customization shall not be applied to the selected food item.

2. The system shall notify the customer of the reason the ingredient removal request could not be completed.

3. Invalid or unauthorized ingredient removal requests shall be rejected without affecting previously valid customization selections, where applicable.

4. The system shall prevent the customer from proceeding to the Add to Cart operation until all ingredient customization validation requirements are satisfied.

5. No restaurant, menu, food item, ingredient, pricing, recipe, or configuration master data shall be modified as a result of the failed ingredient removal request.

6. The customer's existing ordering session shall remain active unless termination is required due to security or system policies.

#### 3.3.17.11 Success Response

Upon successful completion of the Remove Ingredients functionality, the system shall:

1. Display the selected ingredient removal preferences associated with the selected food item.

2. Display the updated food item summary, including all removed ingredients and the remaining ingredient configuration.

3. Display the recalculated food item price, including any applicable pricing adjustments, taxes, service charges, discounts, and the final payable amount, where applicable.

4. Clearly indicate the ingredients that have been removed from the selected food item.

5. Display only valid, approved, active, and customer-removable ingredients associated with the selected food item.

6. Preserve the selected ingredient removal preferences throughout the current ordering session until the food item is added to the cart, removed, or the session expires.

7. Allow the customer to restore, remove, or modify ingredient removal selections before adding the food item to the cart.

8. Allow the customer to proceed to the Add to Cart functionality with the validated ingredient customization.

9. Ensure that removing ingredients does not modify any restaurant, menu, food item, ingredient, pricing, recipe, or configuration master data.

10. Provide a consistent, accurate, and responsive ingredient customization experience across supported devices and platforms.

11. Record ingredient removal activities for analytics, reporting, auditing, recommendation, and product improvement purposes, where applicable.

#### 3.3.17.12 Failure Response

If the Remove Ingredients functionality cannot be completed successfully, the system shall:

1. Inform the customer that the requested ingredient removal could not be completed.

2. Display an appropriate and user-friendly message describing the reason for the failure, where applicable.

3. Highlight invalid, unavailable, restricted, or non-removable ingredients that require customer action, where applicable.

4. Prevent the customer from proceeding to the Add to Cart functionality until all ingredient customization validation requirements and business rules are satisfied.

5. Reject requests to remove mandatory, fixed, unavailable, unpublished, deleted, disabled, inactive, restricted, or otherwise non-removable ingredients.

6. Preserve previously valid ingredient customization selections where possible, unless they become invalid due to business rules or availability changes.

7. Allow the customer to modify or restore ingredient removal selections and retry the request when the failure is recoverable.

8. Record the ingredient removal failure event for system monitoring, diagnostics, auditing, and analytics purposes, where applicable.

9. Ensure that no restaurant, menu, food item, ingredient, pricing, recipe, or configuration master data is modified as a result of the failed ingredient removal request.

10. Maintain the customer's current ordering session and application state unless termination is required due to security or system policies.

#### 3.3.17.13 Acceptance Criteria

The Remove Ingredients functionality shall be considered successfully implemented when all the following conditions are satisfied:

| AC ID | Acceptance Criteria |
|-------|----------------------|
| AC-RI-001 | The customer shall be able to remove approved customer-removable ingredients associated with the selected food item. |
| AC-RI-002 | The system shall display removable ingredients only for food items that are active, published, and available for ordering. |
| AC-RI-003 | The system shall retrieve and display only approved, active, and customer-removable ingredients configured for the selected food item. |
| AC-RI-004 | The system shall clearly distinguish removable ingredients from mandatory or non-removable ingredients. |
| AC-RI-005 | The system shall allow customers to remove one or more eligible ingredients in accordance with the restaurant's customization configuration. |
| AC-RI-006 | The system shall validate that every requested ingredient removal complies with the configured customization rules and business constraints. |
| AC-RI-007 | The system shall prevent customers from removing mandatory, fixed, restricted, unavailable, or non-removable ingredients. |
| AC-RI-008 | The system shall automatically update the food item customization summary whenever ingredient removal selections are added, modified, or restored. |
| AC-RI-009 | The system shall automatically recalculate the food item price whenever ingredient removal affects pricing. |
| AC-RI-010 | The system shall display the updated pricing information, including all applicable pricing adjustments. |
| AC-RI-011 | The system shall preserve the selected ingredient removal preferences throughout the current ordering session until the food item is added to the cart, removed, or the session expires. |
| AC-RI-012 | The customer shall be able to restore or modify removed ingredients before adding the food item to the cart. |
| AC-RI-013 | The system shall ensure that removing ingredients does not modify any restaurant, menu, food item, ingredient, pricing, recipe, or configuration master data. |
| AC-RI-014 | The system shall display an appropriate validation or error message whenever ingredient removal cannot be completed successfully. |
| AC-RI-015 | The system shall record ingredient removal activities for analytics, reporting, auditing, and product improvement purposes, where applicable. |
| AC-RI-016 | The system shall provide a consistent, accurate, and responsive ingredient customization experience across supported devices and platforms. |


### 3.3.18 Mark Item as Favorite

#### 3.3.18.1 Description

This use case allows the customer to mark a food item as a favorite for quick access in future ordering sessions. The system shall allow authenticated customers to add eligible food items to their personal Favorites list. The system shall validate the request, prevent duplicate favorite entries, associate the favorite item with the customer's account, and make it available through the Favorites section without modifying any restaurant, menu, or food item master data.

#### 3.3.18.2 Actors

**Primary Actor:**
- Customer

**Supporting Actors:**
- Favorites Service
- Menu Service
- Restaurant Service
- Customer Profile Service
- Authentication and Authorization Service

#### 3.3.18.3 Preconditions

1. The customer shall be authenticated and have an active QuickBite account.

2. The customer's account shall be active and eligible to use the Favorites functionality.

3. The selected restaurant shall exist and be available on the platform.

4. The selected food item shall exist within the restaurant's latest published menu.

5. The selected food item shall be active, published, and eligible to be marked as a favorite.

6. The Favorites feature shall be enabled for the customer's account.

7. The customer shall have opened the food item details page or another screen where the Mark as Favorite option is available.

8. Required customer profile, restaurant, menu, and food item information shall be successfully retrieved by the system.

9. The system and all required supporting services shall be operational and available.

10. The customer's session shall be active and authorized.

#### 3.3.18.4 Trigger

The use case is triggered when the authenticated customer selects the **Mark as Favorite** option for a selected food item.

#### 3.3.18.5 Input Fields

| Field | Description | Mandatory |
|-------|-------------|-----------|
| Customer ID | Unique identifier of the authenticated customer | Yes |
| Restaurant ID | Unique identifier of the selected restaurant | Yes |
| Food Item ID | Unique identifier of the selected food item | Yes |
| Favorite Status | Indicates whether the food item should be marked as a favorite | Yes |

#### 3.3.18.6 Business Rules

1. The system shall allow only authenticated customers to mark food items as favorites.

2. The system shall allow customers to mark only active, published, and orderable food items as favorites.

3. The system shall retrieve the latest published version of the selected food item before creating the favorite entry.

4. The system shall associate the favorite food item with the authenticated customer's account.

5. The system shall prevent duplicate favorite entries for the same customer and food item.

6. If the selected food item has already been marked as a favorite, the system shall indicate its existing favorite status.

7. The system shall allow customers to remove the food item from their Favorites list through the appropriate functionality.

8. Marking a food item as a favorite shall not automatically add the item to the cart or initiate an order.

9. The system shall preserve the customer's Favorites list across sessions until the customer removes the item or the account is deleted.

10. The system shall prevent customers from marking unavailable, unpublished, deleted, disabled, inactive, or restricted food items as favorites.

11. The system shall synchronize the Favorites list across all supported devices associated with the customer's account.

12. Marking a food item as a favorite shall not modify any restaurant, menu, food item, pricing, inventory, or configuration master data.

13. The system shall record favorite item activities for analytics, reporting, auditing, personalization, recommendation, and product improvement purposes, where applicable.

14. The system shall comply with applicable privacy, data protection, accessibility, security, and regulatory requirements governing customer preference data.

#### 3.3.18.7 Validations

1. The system shall validate that the customer is authenticated and authorized to use the Favorites functionality.

2. The system shall validate that the customer's account exists and is active.

3. The system shall validate that the selected restaurant exists.

4. The system shall validate that the selected food item exists within the restaurant's latest published menu.

5. The system shall validate that the selected food item is active, published, and eligible to be marked as a favorite.

6. The system shall validate that the Favorites feature is enabled for the customer's account.

7. The system shall validate that the selected food item has not already been marked as a favorite by the customer.

8. The system shall validate that unavailable, unpublished, deleted, disabled, inactive, or restricted food items cannot be added to the Favorites list.

9. The system shall validate system availability before processing the favorite item request.

10. The system shall validate that the retrieved customer, restaurant, and food item information is complete and not corrupted before creating the favorite entry.

11. The system shall validate that duplicate favorite entries are not created for the same customer and food item.

12. The system shall validate that marking a food item as a favorite does not modify any restaurant, menu, food item, pricing, inventory, or configuration master data.

13. The system shall display an appropriate validation message whenever the favorite item request violates configured business rules or system constraints.

#### 3.3.18.8 Main Flow

1. The authenticated customer selects a food item from the restaurant menu or food item details page.

2. The customer selects the **Mark as Favorite** option.

3. The system validates the customer's authentication, authorization, and account status.

4. The system retrieves the latest published information for the selected food item.

5. The system validates that the selected food item is active, published, and eligible to be added to the customer's Favorites list.

6. The system checks whether the selected food item already exists in the customer's Favorites list.

7. The system creates a new favorite item association for the customer if no duplicate entry exists.

8. The system stores the favorite item information in the customer's Favorites list.

9. The system updates the favorite status of the selected food item.

10. The system displays a confirmation indicating that the food item has been successfully added to the Favorites list.

11. The system updates the favorite indicator across applicable screens within the current session.

12. The customer continues browsing, customizing, ordering, or viewing the Favorites list.

13. The use case ends successfully.

#### 3.3.18.9 Alternate Flows

##### AF-1: Customer Is Not Authenticated

1. The customer selects the **Mark as Favorite** option.
2. The system determines that the customer is not authenticated.
3. The system prompts the customer to sign in or create an account.
4. The use case ends.

---

##### AF-2: Customer Account Is Inactive

1. The customer attempts to mark a food item as a favorite.
2. The system determines that the customer's account is inactive, suspended, or restricted.
3. The system displays an appropriate error message.
4. The use case ends.

---

##### AF-3: Restaurant Does Not Exist

1. The customer attempts to mark a food item as a favorite.
2. The system determines that the selected restaurant does not exist.
3. The system displays an appropriate error message.
4. The use case ends.

---

##### AF-4: Food Item Does Not Exist

1. The customer attempts to mark a food item as a favorite.
2. The system determines that the selected food item does not exist in the restaurant's latest published menu.
3. The system displays an appropriate error message.
4. The use case ends.

---

##### AF-5: Food Item Is Already Marked as Favorite

1. The customer selects the **Mark as Favorite** option for a food item already present in the Favorites list.
2. The system detects the existing favorite entry.
3. The system informs the customer that the food item has already been marked as a favorite.
4. The use case ends.

---

##### AF-6: Food Item Is No Longer Eligible

1. The customer attempts to mark a food item as a favorite.
2. The system determines that the selected food item is unavailable, unpublished, deleted, disabled, inactive, or restricted.
3. The system prevents the favorite request.
4. The system displays an appropriate validation message.
5. The use case ends.

---

##### AF-7: Favorites Service Is Unavailable

1. The customer requests to mark a food item as a favorite.
2. The system is unable to process the request due to a temporary Favorites Service or system failure.
3. The system displays an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

---

##### AF-8: Favorite Item Creation Fails

1. The customer requests to mark a food item as a favorite.
2. The system encounters an unexpected processing or database error while creating the favorite entry.
3. The system displays an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

#### 3.3.18.10 Postconditions

Upon completion of the Mark Item as Favorite functionality, one of the following postconditions shall apply:

##### Successful Completion

1. The selected food item shall be successfully associated with the authenticated customer's Favorites list.

2. The favorite item record shall be stored and linked to the customer's account.

3. The selected food item shall be displayed as a favorite across applicable screens and supported devices associated with the customer's account.

4. The customer shall be able to access the selected food item from the Favorites section during future ordering sessions.

5. The favorite status of the selected food item shall remain active until the customer explicitly removes it from the Favorites list or the account is deleted.

6. The system shall record favorite item activities for analytics, reporting, auditing, personalization, recommendation, and product improvement purposes, where applicable.

7. No restaurant, menu, food item, pricing, inventory, or configuration master data shall be modified during the favorite item creation process.

##### Unsuccessful Completion

1. The selected food item shall not be added to the customer's Favorites list.

2. The system shall notify the customer of the reason the favorite request could not be completed.

3. Duplicate, invalid, or unauthorized favorite requests shall be rejected without affecting existing favorite entries.

4. No favorite record shall be created for the failed request.

5. No restaurant, menu, food item, pricing, inventory, or configuration master data shall be modified as a result of the failed favorite request.

6. The customer's authenticated session shall remain active unless termination is required due to security or system policies.

#### 3.3.18.11 Success Response

Upon successful completion of the Mark Item as Favorite functionality, the system shall:

1. Display a confirmation indicating that the selected food item has been successfully added to the customer's Favorites list.

2. Display the selected food item with its updated favorite status.

3. Update the favorite indicator consistently across all applicable screens within the current session.

4. Make the selected food item available in the customer's Favorites section.

5. Prevent duplicate favorite entries for the same customer and food item.

6. Preserve the favorite status across future sessions and supported customer devices.

7. Allow the customer to remove the food item from the Favorites list through the appropriate functionality.

8. Ensure that marking a food item as a favorite does not add the item to the cart or initiate an order.

9. Ensure that marking a food item as a favorite does not modify any restaurant, menu, food item, pricing, inventory, or configuration master data.

10. Provide a consistent, accurate, and responsive Favorites experience across supported devices and platforms.

11. Record favorite item activities for analytics, reporting, auditing, personalization, recommendation, and product improvement purposes, where applicable.

#### 3.3.18.12 Failure Response

If the Mark Item as Favorite functionality cannot be completed successfully, the system shall:

1. Inform the customer that the requested favorite item operation could not be completed.

2. Display an appropriate and user-friendly message describing the reason for the failure, where applicable.

3. Prompt the customer to sign in if authentication is required before marking a food item as a favorite.

4. Reject duplicate favorite requests for food items that already exist in the customer's Favorites list.

5. Prevent unavailable, unpublished, deleted, disabled, inactive, restricted, or invalid food items from being added to the Favorites list.

6. Preserve all existing favorite items without modification when the current favorite request fails.

7. Allow the customer to retry the favorite request when the failure is recoverable.

8. Record the favorite item failure event for system monitoring, diagnostics, auditing, analytics, and security purposes, where applicable.

9. Ensure that no restaurant, menu, food item, pricing, inventory, customer profile, or configuration master data is modified as a result of the failed favorite request.

10. Maintain the customer's authenticated session and current application state unless termination is required due to security or system policies.

#### 3.3.18.13 Acceptance Criteria

The Mark Item as Favorite functionality shall be considered successfully implemented when all the following conditions are satisfied:

| AC ID | Acceptance Criteria |
|-------|----------------------|
| AC-MIF-001 | Only authenticated customers shall be able to mark food items as favorites. |
| AC-MIF-002 | The system shall allow only active, published, and orderable food items to be marked as favorites. |
| AC-MIF-003 | The system shall associate the favorite food item with the authenticated customer's account. |
| AC-MIF-004 | The system shall prevent duplicate favorite entries for the same customer and food item. |
| AC-MIF-005 | The system shall display the current favorite status of the selected food item. |
| AC-MIF-006 | The system shall update the favorite indicator consistently across all applicable screens after the item is marked as a favorite. |
| AC-MIF-007 | The system shall make the selected food item available in the customer's Favorites list immediately after successful completion. |
| AC-MIF-008 | The system shall synchronize the customer's Favorites list across all supported devices associated with the customer's account. |
| AC-MIF-009 | The system shall preserve favorite items across customer sessions until they are explicitly removed or the account is deleted. |
| AC-MIF-010 | The system shall prevent unavailable, unpublished, deleted, disabled, inactive, restricted, or invalid food items from being marked as favorites. |
| AC-MIF-011 | The customer shall be able to remove the food item from the Favorites list through the appropriate functionality. |
| AC-MIF-012 | Marking a food item as a favorite shall not automatically add the item to the cart or initiate an order. |
| AC-MIF-013 | The system shall ensure that marking a food item as a favorite does not modify any restaurant, menu, food item, pricing, inventory, customer profile, or configuration master data. |
| AC-MIF-014 | The system shall display an appropriate validation or error message whenever the favorite request cannot be completed successfully. |
| AC-MIF-015 | The system shall record favorite item activities for analytics, reporting, auditing, personalization, recommendation, and product improvement purposes, where applicable. |
| AC-MIF-016 | The system shall provide a consistent, accurate, and responsive Favorites experience across supported devices and platforms. |

### 3.3.19 Remove Item from Favorites

#### 3.3.19.1 Description

This use case allows an authenticated customer to remove a previously saved food item from their Favorites list. The system shall validate the removal request, ensure that the selected food item exists in the customer's Favorites list, remove the favorite association from the customer's account, and update the Favorites list across all supported devices without modifying any restaurant, menu, food item, pricing, inventory, or other master data.

#### 3.3.19.2 Actors

**Primary Actor:**
- Customer

**Supporting Actors:**
- Favorites Service
- Menu Service
- Restaurant Service
- Customer Profile Service
- Authentication and Authorization Service

#### 3.3.19.3 Preconditions

1. The customer shall be authenticated and have an active QuickBite account.

2. The customer's account shall be active and eligible to use the Favorites functionality.

3. The selected food item shall already exist in the customer's Favorites list.

4. The selected restaurant shall exist and be available on the platform.

5. The selected food item shall exist within the restaurant's latest published menu or shall have a valid favorite record associated with the customer.

6. The Favorites feature shall be enabled for the customer's account.

7. The customer shall have opened the Favorites list or another screen where the Remove from Favorites option is available.

8. Required customer profile, favorite item, restaurant, and food item information shall be successfully retrieved by the system.

9. The system and all required supporting services shall be operational and available.

10. The customer's session shall be active and authorized.

#### 3.3.19.4 Trigger

The use case is triggered when the authenticated customer selects the **Remove from Favorites** option for a food item that exists in the customer's Favorites list.

#### 3.3.19.5 Input Fields

| Field | Description | Mandatory |
|-------|-------------|-----------|
| Customer ID | Unique identifier of the authenticated customer | Yes |
| Restaurant ID | Unique identifier of the restaurant associated with the favorite food item | Yes |
| Food Item ID | Unique identifier of the food item to be removed from the Favorites list | Yes |
| Favorite Status | Indicates whether the food item should be removed from the Favorites list | Yes |

#### 3.3.19.6 Business Rules

1. The system shall allow only authenticated customers to remove food items from their Favorites list.

2. The system shall allow removal only for food items that currently exist in the authenticated customer's Favorites list.

3. The system shall validate the customer's ownership of the favorite item before processing the removal request.

4. The system shall remove only the association between the customer and the selected favorite food item.

5. Removing a food item from the Favorites list shall not affect the restaurant's menu, food item, pricing, inventory, or availability.

6. Removing a favorite item shall not delete or modify the food item from the platform.

7. The system shall immediately update the favorite status of the selected food item across all applicable screens.

8. The system shall synchronize the updated Favorites list across all supported devices associated with the customer's account.

9. Removing a favorite item shall not remove the item from the customer's cart, order history, recently viewed items, or active orders.

10. The system shall prevent customers from removing food items that are not present in their Favorites list.

11. The system shall preserve all remaining favorite items without modification.

12. The system shall record favorite removal activities for analytics, reporting, auditing, personalization, recommendation, and product improvement purposes, where applicable.

13. Removing a favorite item shall not modify any restaurant, menu, food item, pricing, inventory, customer profile, or configuration master data.

14. The system shall comply with applicable privacy, data protection, accessibility, security, retention, and regulatory requirements governing customer preference data.

---

#### 3.3.19.7 Validations

1. The system shall validate that the customer is authenticated and authorized to use the Favorites functionality.

2. The system shall validate that the customer's account exists and is active.

3. The system shall validate that the selected restaurant exists, where applicable.

4. The system shall validate that the selected food item exists or has a valid favorite association with the authenticated customer.

5. The system shall validate that the selected food item currently exists in the customer's Favorites list.

6. The system shall validate that the customer is authorized to remove only their own favorite items.

7. The system shall validate that duplicate removal requests for the same favorite item are not processed.

8. The system shall validate that the selected favorite item has not already been removed.

9. The system shall validate system availability before processing the favorite removal request.

10. The system shall validate that the retrieved customer, favorite item, restaurant, and food item information is complete and not corrupted.

11. The system shall validate that removing a favorite item does not modify any restaurant, menu, food item, pricing, inventory, customer profile, or configuration master data.

12. The system shall display an appropriate validation message whenever the favorite removal request violates configured business rules or system constraints.

---

#### 3.3.19.8 Main Flow

1. The authenticated customer opens the Favorites list or another screen displaying favorite food items.

2. The customer selects a food item to remove from the Favorites list.

3. The customer selects the **Remove from Favorites** option.

4. The system validates the customer's authentication, authorization, and account status.

5. The system retrieves the selected favorite item information.

6. The system validates that the selected food item currently exists in the customer's Favorites list.

7. The system removes the favorite association between the customer and the selected food item.

8. The system updates the customer's Favorites list.

9. The system updates the favorite status of the selected food item across applicable screens.

10. The system synchronizes the updated Favorites list across supported customer devices.

11. The system displays a confirmation indicating that the food item has been successfully removed from the Favorites list.

12. The customer continues browsing, ordering, or managing the remaining favorite items.

13. The use case ends successfully.

#### 3.3.19.9 Alternate Flows

##### AF-1: Customer Is Not Authenticated

1. The customer selects the **Remove from Favorites** option.
2. The system determines that the customer is not authenticated.
3. The system prompts the customer to sign in.
4. The use case ends.

---

##### AF-2: Customer Account Is Inactive

1. The customer attempts to remove a food item from the Favorites list.
2. The system determines that the customer's account is inactive, suspended, or restricted.
3. The system displays an appropriate error message.
4. The use case ends.

---

##### AF-3: Food Item Is Not Present in Favorites

1. The customer attempts to remove a food item from the Favorites list.
2. The system determines that the selected food item does not exist in the customer's Favorites list.
3. The system displays an appropriate validation message.
4. The use case ends.

---

##### AF-4: Favorite Item Has Already Been Removed

1. The customer submits a remove request.
2. The system determines that the favorite item has already been removed.
3. The system informs the customer that the selected food item is no longer available in the Favorites list.
4. The use case ends.

---

##### AF-5: Unauthorized Favorite Removal Request

1. The customer attempts to remove a favorite item that does not belong to their account.
2. The system detects an unauthorized removal request.
3. The system rejects the request.
4. The system displays an appropriate error message.
5. The use case ends.

---

##### AF-6: Favorites Service Is Unavailable

1. The customer requests to remove a food item from the Favorites list.
2. The system is unable to process the request due to a temporary Favorites Service or system failure.
3. The system displays an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

---

##### AF-7: Favorite Removal Processing Fails

1. The customer requests to remove a favorite item.
2. The system encounters an unexpected processing or database error while removing the favorite association.
3. The system displays an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

---

#### 3.3.19.10 Postconditions

Upon completion of the Remove Item from Favorites functionality, one of the following postconditions shall apply:

##### Successful Completion

1. The selected food item shall be successfully removed from the authenticated customer's Favorites list.

2. The favorite association between the customer and the selected food item shall be permanently removed.

3. The Favorites list shall be updated immediately across all applicable screens and supported devices.

4. The selected food item shall no longer appear in the customer's Favorites list.

5. The customer shall continue to access all remaining favorite food items without interruption.

6. The system shall record favorite removal activities for analytics, reporting, auditing, personalization, recommendation, and product improvement purposes, where applicable.

7. No restaurant, menu, food item, pricing, inventory, customer profile, or configuration master data shall be modified during the favorite removal process.

##### Unsuccessful Completion

1. The selected food item shall remain in the customer's Favorites list.

2. The system shall notify the customer of the reason the favorite removal request could not be completed.

3. Invalid or unauthorized favorite removal requests shall be rejected without affecting existing favorite items.

4. No favorite association shall be removed for the failed request.

5. No restaurant, menu, food item, pricing, inventory, customer profile, or configuration master data shall be modified as a result of the failed favorite removal request.

6. The customer's authenticated session shall remain active unless termination is required due to security or system policies.

---

#### 3.3.19.11 Success Response

Upon successful completion of the Remove Item from Favorites functionality, the system shall:

1. Display a confirmation indicating that the selected food item has been successfully removed from the Favorites list.

2. Remove the selected food item from the customer's Favorites list.

3. Update the favorite indicator consistently across all applicable screens within the current session.

4. Synchronize the updated Favorites list across all supported customer devices.

5. Preserve all remaining favorite items without modification.

6. Allow the customer to mark the same food item as a favorite again in the future.

7. Ensure that removing a favorite item does not remove the item from the cart, active orders, order history, or recently viewed items.

8. Ensure that removing a favorite item does not modify any restaurant, menu, food item, pricing, inventory, customer profile, or configuration master data.

9. Provide a consistent, accurate, and responsive Favorites management experience across supported devices and platforms.

10. Record favorite removal activities for analytics, reporting, auditing, personalization, recommendation, and product improvement purposes, where applicable.

---

#### 3.3.19.12 Failure Response

If the Remove Item from Favorites functionality cannot be completed successfully, the system shall:

1. Inform the customer that the requested favorite removal operation could not be completed.

2. Display an appropriate and user-friendly message describing the reason for the failure, where applicable.

3. Prompt the customer to sign in if authentication is required before removing a favorite item.

4. Prevent removal requests for food items that do not exist in the customer's Favorites list.

5. Reject unauthorized requests to remove favorite items belonging to another customer.

6. Preserve all existing favorite items without modification when the removal request fails.

7. Allow the customer to retry the removal request when the failure is recoverable.

8. Record the favorite removal failure event for system monitoring, diagnostics, auditing, analytics, and security purposes, where applicable.

9. Ensure that no restaurant, menu, food item, pricing, inventory, customer profile, or configuration master data is modified as a result of the failed favorite removal request.

10. Maintain the customer's authenticated session and current application state unless termination is required due to security or system policies.

---

#### 3.3.19.13 Acceptance Criteria

The Remove Item from Favorites functionality shall be considered successfully implemented when all the following conditions are satisfied:

| AC ID | Acceptance Criteria |
|-------|----------------------|
| AC-RIF-001 | Only authenticated customers shall be able to remove food items from their Favorites list. |
| AC-RIF-002 | The system shall allow removal only for food items that currently exist in the authenticated customer's Favorites list. |
| AC-RIF-003 | The system shall validate that the customer is authorized to remove only their own favorite items. |
| AC-RIF-004 | The system shall permanently remove the association between the customer and the selected favorite food item. |
| AC-RIF-005 | The system shall immediately update the favorite indicator across all applicable screens after successful removal. |
| AC-RIF-006 | The system shall remove the selected food item from the customer's Favorites list. |
| AC-RIF-007 | The system shall synchronize the updated Favorites list across all supported customer devices. |
| AC-RIF-008 | The system shall preserve all remaining favorite items without modification. |
| AC-RIF-009 | The system shall allow the customer to mark the same food item as a favorite again after removal. |
| AC-RIF-010 | The system shall prevent removal requests for food items that do not exist in the customer's Favorites list. |
| AC-RIF-011 | The system shall reject unauthorized requests to remove another customer's favorite items. |
| AC-RIF-012 | Removing a favorite item shall not remove the food item from the cart, active orders, order history, or recently viewed items. |
| AC-RIF-013 | The system shall ensure that removing a favorite item does not modify any restaurant, menu, food item, pricing, inventory, customer profile, or configuration master data. |
| AC-RIF-014 | The system shall display an appropriate validation or error message whenever the favorite removal request cannot be completed successfully. |
| AC-RIF-015 | The system shall record favorite removal activities for analytics, reporting, auditing, personalization, recommendation, and product improvement purposes, where applicable. |
| AC-RIF-016 | The system shall provide a consistent, accurate, and responsive Favorites management experience across supported devices and platforms. |

### 3.3.20 View Favorite Items

#### 3.3.20.1 Description

This use case allows an authenticated customer to view all food items that have been saved in their personal Favorites list. The system shall retrieve and display the customer's latest favorite food items together with relevant restaurant and food item information, including current availability, pricing, and favorite status. The Favorites list shall enable the customer to quickly access preferred food items for viewing, customization, or ordering without modifying any restaurant, menu, food item, pricing, inventory, customer profile, or configuration master data.

#### 3.3.20.2 Actors

**Primary Actor:**
- Customer

**Supporting Actors:**
- Favorites Service
- Menu Service
- Restaurant Service
- Customer Profile Service
- Pricing Service
- Authentication and Authorization Service

#### 3.3.20.3 Preconditions

1. The customer shall be authenticated and have an active QuickBite account.

2. The customer's account shall be active and authorized to access the Favorites functionality.

3. The Favorites feature shall be enabled for the customer's account.

4. The customer shall have at least one favorite food item or be permitted to view an empty Favorites list.

5. Required customer profile, restaurant, menu, favorite item, pricing, and availability information shall be successfully retrievable by the system.

6. The customer shall have opened the Favorites section of the application.

7. The system and all required supporting services shall be operational and available.

8. The customer's authenticated session shall be active.

#### 3.3.20.4 Trigger

The use case is triggered when the authenticated customer opens the **Favorites** section to view the list of saved favorite food items.

#### 3.3.20.5 Input Fields

| Field | Description | Mandatory |
|-------|-------------|-----------|
| Customer ID | Unique identifier of the authenticated customer | Yes |
| Favorite Status | Indicates retrieval of favorite food items | Yes |
| Page Number | Page number for paginated results, where supported | No |
| Page Size | Number of favorite items per page, where supported | No |
| Sort Option | Preferred sorting option for favorite items, where supported | No |
| Search Keyword | Keyword to search within favorite items, where supported | No |

#### 3.3.20.6 Business Rules

1. The system shall allow only authenticated customers to access their Favorites list.

2. The system shall retrieve only the favorite food items associated with the authenticated customer's account.

3. The system shall display the latest available information for each favorite food item.

4. The system shall display the associated restaurant information for every favorite food item.

5. The system shall display the current availability status of each favorite food item.

6. The system shall display the latest applicable food item price in accordance with the restaurant's current pricing.

7. The system shall clearly indicate whether a favorite food item is currently available for ordering.

8. The system shall allow customers to search, sort, and browse favorite food items where such functionality is supported.

9. The system shall allow customers to open a favorite food item for viewing, customization, ordering, or removal from the Favorites list.

10. If the customer has no favorite food items, the system shall display a platform-defined message indicating that the Favorites list is empty.

11. The system shall synchronize the Favorites list across all supported devices associated with the customer's account.

12. Viewing the Favorites list shall not modify any favorite item, restaurant, menu, food item, pricing, inventory, customer profile, or configuration master data.

13. The system shall record Favorites viewing activities for analytics, reporting, auditing, personalization, recommendation, and product improvement purposes, where applicable.

14. The system shall comply with applicable privacy, accessibility, security, data protection, and regulatory requirements governing customer preference information.

#### 3.3.20.7 Validations

1. The system shall validate that the customer is authenticated and authorized to access the Favorites functionality.

2. The system shall validate that the customer's account exists and is active.

3. The system shall validate that the Favorites feature is enabled for the customer's account.

4. The system shall validate that only favorite food items associated with the authenticated customer's account are retrieved.

5. The system shall validate that the latest restaurant, food item, pricing, and availability information is retrieved before displaying the Favorites list.

6. The system shall validate that unavailable, unpublished, deleted, disabled, or inactive food items are appropriately identified within the Favorites list.

7. The system shall validate pagination parameters, where pagination is supported.

8. The system shall validate sorting options against the supported sorting criteria, where sorting is requested.

9. The system shall validate search keywords before processing favorite item search requests, where search functionality is supported.

10. The system shall validate system availability before retrieving the Favorites list.

11. The system shall validate that the retrieved Favorites information is complete and not corrupted before displaying it to the customer.

12. The system shall validate that viewing the Favorites list does not modify any favorite item, restaurant, menu, food item, pricing, inventory, customer profile, or configuration master data.

13. The system shall display a platform-defined message when the customer has no favorite food items.

14. The system shall display an appropriate validation message whenever the Favorites retrieval request violates configured business rules or system constraints.

#### 3.3.20.8 Main Flow

1. The authenticated customer navigates to the **Favorites** section of the QuickBite platform.

2. The system validates the customer's authentication, authorization, and account status.

3. The system retrieves all favorite food items associated with the authenticated customer's account.

4. The system retrieves the latest restaurant, food item, pricing, availability, and favorite status information for each favorite food item.

5. The system displays the customer's Favorites list.

6. The system displays each favorite food item together with applicable details, including:
   - Food Item Name
   - Restaurant Name
   - Food Image
   - Current Price
   - Availability Status
   - Favorite Indicator
   - Other applicable food item information

7. The customer browses the Favorites list.

8. The customer searches, sorts, or navigates through favorite food items, where supported.

9. The customer selects a favorite food item.

10. The system opens the selected food item's details page.

11. The customer may continue to customize the food item, add it to the cart, place an order, or remove it from the Favorites list.

12. The system records the Favorites viewing activity, where applicable.

13. The use case ends successfully.

---

#### 3.3.20.9 Alternate Flows

##### AF-1: Customer Is Not Authenticated

1. The customer attempts to access the Favorites section.
2. The system determines that the customer is not authenticated.
3. The system prompts the customer to sign in.
4. The use case ends.

---

##### AF-2: Customer Account Is Inactive

1. The customer attempts to access the Favorites list.
2. The system determines that the customer's account is inactive, suspended, or restricted.
3. The system displays an appropriate error message.
4. The use case ends.

---

##### AF-3: Favorites List Is Empty

1. The customer opens the Favorites section.
2. The system determines that no favorite food items exist for the authenticated customer.
3. The system displays a platform-defined message indicating that the Favorites list is empty.
4. The system may display recommended food items, where applicable.
5. The use case ends.

---

##### AF-4: Food Item Is No Longer Available

1. The customer views the Favorites list.
2. The system determines that one or more favorite food items are unavailable, unpublished, deleted, disabled, or inactive.
3. The system clearly indicates the current availability status of the affected food items.
4. The customer may continue viewing other available favorite items.
5. The use case continues.

---

##### AF-5: Restaurant Is No Longer Available

1. The customer views the Favorites list.
2. The system determines that the associated restaurant is inactive, closed, or unavailable.
3. The system displays the appropriate restaurant availability status.
4. The customer may continue viewing remaining favorite items.
5. The use case continues.

---

##### AF-6: Favorites Service Is Unavailable

1. The customer requests the Favorites list.
2. The system is unable to retrieve the Favorites information due to a temporary Favorites Service or system failure.
3. The system displays an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

---

##### AF-7: Favorites Retrieval Fails

1. The customer requests the Favorites list.
2. The system encounters an unexpected processing or database error while retrieving favorite items.
3. The system displays an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

#### 3.3.20.10 Postconditions

Upon completion of the View Favorite Items functionality, one of the following postconditions shall apply:

##### Successful Completion

1. The customer's Favorites list shall be successfully retrieved and displayed.

2. The latest restaurant, food item, pricing, availability, and favorite status information shall be presented for each favorite food item.

3. The customer shall be able to view, browse, search, sort, and select favorite food items, where supported.

4. The customer shall be able to navigate to the selected food item's details page for further actions such as customization, ordering, or removing the item from the Favorites list.

5. The Favorites list shall remain synchronized across all supported devices associated with the customer's account.

6. The system shall record Favorites viewing activities for analytics, reporting, auditing, personalization, recommendation, and product improvement purposes, where applicable.

7. No favorite item, restaurant, menu, food item, pricing, inventory, customer profile, or configuration master data shall be modified during the Favorites viewing process.

##### Unsuccessful Completion

1. The Favorites list shall not be displayed.

2. The system shall notify the customer of the reason the Favorites list could not be retrieved.

3. Previously stored favorite item information shall remain unchanged.

4. No favorite item, restaurant, menu, food item, pricing, inventory, customer profile, or configuration master data shall be modified as a result of the failed Favorites retrieval request.

5. The customer's authenticated session shall remain active unless termination is required due to security or system policies.

---

#### 3.3.20.11 Success Response

Upon successful completion of the View Favorite Items functionality, the system shall:

1. Display all favorite food items associated with the authenticated customer's account.

2. Display the latest restaurant information, food item information, pricing, and availability status for each favorite food item.

3. Clearly indicate the favorite status of every displayed food item.

4. Display the current ordering availability for each favorite food item.

5. Allow the customer to browse, search, sort, and navigate through favorite food items, where supported.

6. Allow the customer to open a selected favorite food item for viewing, customization, ordering, or removal from the Favorites list.

7. Synchronize the Favorites list across all supported customer devices.

8. Ensure that viewing favorite items does not modify any favorite item, restaurant, menu, food item, pricing, inventory, customer profile, or configuration master data.

9. Provide a consistent, accurate, and responsive Favorites viewing experience across supported devices and platforms.

10. Record Favorites viewing activities for analytics, reporting, auditing, personalization, recommendation, and product improvement purposes, where applicable.

---

#### 3.3.20.12 Failure Response

If the View Favorite Items functionality cannot be completed successfully, the system shall:

1. Inform the customer that the Favorites list could not be retrieved.

2. Display an appropriate and user-friendly message describing the reason for the failure, where applicable.

3. Prompt the customer to sign in if authentication is required before accessing the Favorites list.

4. Display a platform-defined message if no favorite food items exist for the authenticated customer.

5. Preserve all existing favorite items without modification when the retrieval request fails.

6. Allow the customer to retry the Favorites retrieval request when the failure is recoverable.

7. Record the Favorites retrieval failure event for system monitoring, diagnostics, auditing, analytics, and security purposes, where applicable.

8. Ensure that no favorite item, restaurant, menu, food item, pricing, inventory, customer profile, or configuration master data is modified as a result of the failed retrieval request.

9. Maintain the customer's authenticated session and current application state unless termination is required due to security or system policies.

---

#### 3.3.20.13 Acceptance Criteria

The View Favorite Items functionality shall be considered successfully implemented when all the following conditions are satisfied:

| AC ID | Acceptance Criteria |
|-------|----------------------|
| AC-VFI-001 | Only authenticated customers shall be able to access their Favorites list. |
| AC-VFI-002 | The system shall retrieve only favorite food items associated with the authenticated customer's account. |
| AC-VFI-003 | The system shall display the latest restaurant, food item, pricing, and availability information for each favorite food item. |
| AC-VFI-004 | The system shall clearly display the favorite status of every favorite food item. |
| AC-VFI-005 | The system shall display the current ordering availability for each favorite food item. |
| AC-VFI-006 | The customer shall be able to browse, search, sort, and navigate favorite food items where supported. |
| AC-VFI-007 | The customer shall be able to open a favorite food item for viewing, customization, ordering, or removal from the Favorites list. |
| AC-VFI-008 | The system shall display a platform-defined message when the customer's Favorites list is empty. |
| AC-VFI-009 | The system shall synchronize the Favorites list across all supported customer devices. |
| AC-VFI-010 | The system shall clearly identify unavailable, unpublished, deleted, disabled, inactive, or restricted favorite food items. |
| AC-VFI-011 | Viewing favorite items shall not modify any favorite item, restaurant, menu, food item, pricing, inventory, customer profile, or configuration master data. |
| AC-VFI-012 | The system shall preserve all favorite items unless explicitly modified through the appropriate Favorites management functionality. |
| AC-VFI-013 | The system shall display an appropriate validation or error message whenever the Favorites retrieval request cannot be completed successfully. |
| AC-VFI-014 | The system shall record Favorites viewing activities for analytics, reporting, auditing, personalization, recommendation, and product improvement purposes, where applicable. |
| AC-VFI-015 | The system shall provide a consistent, accurate, and responsive Favorites viewing experience across supported devices and platforms. |
| AC-VFI-016 | The system shall ensure that only authorized customers can view their own Favorites list. |

### 3.3.21 View Recommended Items

#### 3.3.21.1 Description

This use case allows an authenticated or guest customer to view food item recommendations generated by the QuickBite platform. The system shall retrieve and display personalized or generic recommended food items based on factors such as customer preferences, previous orders, browsing history, favorite items, restaurant popularity, trending items, seasonal offers, location, availability, and platform recommendation algorithms. The Recommendations section shall help customers discover relevant food items and improve the ordering experience without modifying any restaurant, menu, food item, pricing, inventory, customer profile, recommendation rules, or configuration master data.

#### 3.3.21.2 Actors

**Primary:**

- Customer

**Supporting:**

- Recommendation Service
- Customer Profile Service
- Order History Service
- Favorites Service
- Menu Service
- Restaurant Service
- Pricing Service
- Inventory Service
- Location Service
- Authentication and Authorization Service

#### 3.3.21.3 Preconditions

1. The QuickBite platform shall be available.

2. The Recommendation Service shall be operational.

3. The customer may be authenticated or accessing the platform as a guest, subject to platform configuration.

4. Required menu, restaurant, pricing, inventory, and recommendation data shall be available.

5. Customer profile, browsing history, order history, or favorite item information shall be available for personalized recommendations, where applicable.

6. The customer's current delivery location shall be available, where location-based recommendations are supported.

7. The customer accesses the Recommendations section or a page containing recommended food items.

8. All dependent services required to retrieve recommendation data shall be operational.

#### 3.3.21.4 Trigger

The customer opens a page or section that displays recommended food items, or the system automatically loads recommendations during customer interaction.

#### 3.3.21.5 Input Fields

| Field | Description | Mandatory |
|-------|-------------|-----------|
| Customer ID | Unique customer identifier (for authenticated customers) | No |
| Session ID | Guest session identifier | No |
| Current Location | Customer delivery location | No |
| Recommendation Type | Personalized, Trending, Popular, Similar Items, etc. | No |
| Restaurant ID | Restaurant context for recommendations | No |
| Food Item ID | Food item context for similar recommendations | No |
| Page Number | Pagination number | No |
| Page Size | Number of records per page | No |
| Device Information | Device details for analytics | No |

#### 3.3.21.6 Business Rules

1. The system shall display recommended food items based on the platform's recommendation engine.

2. The system shall provide personalized recommendations for authenticated customers whenever sufficient customer activity data is available.

3. If personalized recommendations cannot be generated, the system shall display generic recommendations such as trending, popular, highly rated, or featured food items.

4. The recommendation engine may consider one or more of the following factors:
   - Previous Orders
   - Favorite Items
   - Browsing History
   - Frequently Ordered Items
   - Customer Preferences
   - Cuisine Preferences
   - Restaurant Popularity
   - Food Ratings
   - Trending Items
   - Seasonal Promotions
   - Location
   - Time of Day
   - Ongoing Campaigns
   - Platform Recommendation Rules

5. The system shall recommend only food items that are currently visible and available on the platform.

6. The system shall display the latest food item information, restaurant information, pricing, availability, ratings, and applicable promotional information.

7. The system shall not recommend food items from restaurants that are permanently disabled, unpublished, or restricted.

8. Location-based recommendations shall consider restaurants that are capable of delivering to the customer's selected delivery location, where applicable.

9. The system may periodically refresh recommendations based on customer activity and updated recommendation data.

10. The customer shall be able to select any recommended food item to view its detailed information.

11. Viewing recommended items shall not automatically add any food item to the cart, favorites, or order history.

12. Viewing recommended items shall not modify any restaurant, menu, food item, pricing, inventory, customer profile, recommendation rules, or configuration master data.

13. The system shall record recommendation viewing activities for analytics, personalization, reporting, auditing, machine learning improvement, and product optimization purposes, where applicable.

14. The recommendation process shall comply with applicable privacy, security, accessibility, and data protection requirements.

#### 3.3.21.7 Validations

1. The system shall validate that the Recommendation Service is available before processing the recommendation request.

2. The system shall validate the customer's authentication status when personalized recommendations are requested.

3. The system shall validate the customer's account status before retrieving personalized recommendation data, where authentication is required.

4. The system shall validate the availability of customer profile, order history, browsing history, favorite items, and preference data before generating personalized recommendations.

5. The system shall validate the customer's delivery location before retrieving location-based recommendations, where applicable.

6. The system shall validate that recommended food items are active, published, and available for customer viewing.

7. The system shall validate that associated restaurants are active, operational, and eligible to receive customer orders.

8. The system shall validate the latest pricing, inventory, and availability information before displaying recommended food items.

9. The system shall validate pagination parameters when paginated recommendations are requested.

10. The system shall validate the requested recommendation type against the supported recommendation categories.

11. The system shall validate that recommendation results are successfully retrieved before displaying them to the customer.

12. The system shall validate that incomplete, duplicate, corrupted, or invalid recommendation records are excluded from the displayed results.

13. The system shall validate that viewing recommended items does not modify any restaurant, menu, food item, pricing, inventory, customer profile, recommendation rules, or configuration master data.

14. The system shall display an appropriate validation or error message whenever recommendation retrieval cannot be completed successfully.

#### 3.3.21.8 Main Flow

1. The customer navigates to a page or section that displays recommended food items.

2. The system validates the recommendation request and verifies the availability of the Recommendation Service.

3. The system determines whether the customer is authenticated or accessing the platform as a guest.

4. If the customer is authenticated, the system retrieves relevant customer information, including profile preferences, order history, favorite items, browsing history, and other applicable recommendation inputs.

5. If the customer is a guest or insufficient personalization data is available, the system prepares generic recommendation criteria.

6. The system generates recommended food items using the configured recommendation engine.

7. The system retrieves the latest restaurant information, food item details, pricing, ratings, availability, promotional information, and delivery eligibility for each recommended item.

8. The system filters out unavailable, unpublished, inactive, restricted, or ineligible food items.

9. The system displays the recommended food items to the customer.

10. For each recommended food item, the system displays applicable information, including:
    - Food Item Name
    - Restaurant Name
    - Food Image
    - Current Price
    - Customer Rating
    - Availability Status
    - Delivery Availability
    - Applicable Offers or Discounts
    - Recommendation Label (where applicable, such as Trending, Popular, Recommended for You, Similar Items, Best Seller)

11. The customer browses the recommended food items.

12. The customer selects a recommended food item.

13. The system opens the selected food item's details page.

14. The customer may continue to customize the food item, add it to the cart, mark it as a favorite, or place an order.

15. The system records recommendation viewing activities for analytics, personalization, reporting, auditing, and recommendation model improvement, where applicable.

16. The use case ends successfully.

---

#### 3.3.21.9 Alternate Flows

##### AF-1: Customer Is Not Authenticated

1. The customer accesses the Recommendations section without authentication.
2. The system retrieves generic recommendation data.
3. The system displays generic recommended food items.
4. The use case continues.

---

##### AF-2: Personalized Recommendation Data Is Unavailable

1. The system is unable to retrieve sufficient customer preference, browsing history, favorite items, or order history.
2. The system generates generic recommendations based on platform-defined recommendation rules.
3. The system displays the available recommendations.
4. The use case continues.

---

##### AF-3: No Recommendations Available

1. The system determines that no recommendation data is available.
2. The system displays a platform-defined message indicating that recommendations are currently unavailable.
3. The system may display popular or trending food items instead.
4. The use case ends.

---

##### AF-4: Food Item Is No Longer Available

1. During recommendation processing, the system determines that one or more recommended food items are unavailable, unpublished, inactive, deleted, or restricted.
2. The system excludes the affected food items from the recommendation results or clearly indicates their availability status.
3. The remaining valid recommendations are displayed.
4. The use case continues.

---

##### AF-5: Restaurant Cannot Deliver to Customer Location

1. The system determines that one or more recommended restaurants do not deliver to the customer's selected delivery location.
2. The system excludes those recommendations or clearly indicates delivery unavailability, according to platform configuration.
3. The remaining eligible recommendations are displayed.
4. The use case continues.

---

##### AF-6: Recommendation Service Is Unavailable

1. The customer requests recommended food items.
2. The Recommendation Service is temporarily unavailable.
3. The system displays an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

---

##### AF-7: Recommendation Retrieval Fails

1. The system encounters an unexpected processing, database, or network error while retrieving recommendations.
2. The system logs the failure.
3. The system displays an appropriate error message.
4. The customer may retry the request.
5. The use case ends.

#### 3.3.21.10 Postconditions

Upon completion of the View Recommended Items functionality, one of the following postconditions shall apply:

##### Successful Completion

1. Recommended food items shall be successfully retrieved and displayed to the customer.

2. The displayed recommendations shall include the latest available restaurant information, food item details, pricing, ratings, availability, delivery eligibility, and applicable promotional information.

3. The customer shall be able to browse and view the recommended food items.

4. The customer shall be able to select a recommended food item to navigate to its detailed information page.

5. The customer shall be able to continue with applicable actions such as customization, adding the item to the cart, marking it as a favorite, or placing an order.

6. Recommendation viewing activities shall be recorded for analytics, reporting, auditing, personalization, recommendation model improvement, and product optimization purposes, where applicable.

7. Viewing recommended items shall not modify any restaurant, menu, food item, pricing, inventory, customer profile, recommendation rules, or configuration master data.

##### Unsuccessful Completion

1. Recommended food items shall not be displayed.

2. The system shall notify the customer that recommendations could not be retrieved.

3. Existing recommendation data, customer preferences, and recommendation rules shall remain unchanged.

4. No restaurant, menu, food item, pricing, inventory, customer profile, recommendation rules, or configuration master data shall be modified as a result of the failed recommendation retrieval request.

5. The customer's authenticated session shall remain active unless termination is required by platform security or system policies.

---

#### 3.3.21.11 Success Response

Upon successful completion of the View Recommended Items functionality, the system shall:

1. Display recommended food items generated by the platform recommendation engine.

2. Display the latest restaurant information, food item details, pricing, ratings, availability, delivery eligibility, and applicable promotional information.

3. Clearly identify recommendation labels such as **Recommended for You**, **Trending**, **Popular**, **Best Seller**, or **Similar Items**, where applicable.

4. Display only eligible and currently available food items.

5. Allow the customer to browse and select any recommended food item.

6. Navigate the customer to the selected food item's details page upon selection.

7. Allow the customer to continue with customization, adding the item to the cart, marking it as a favorite, or placing an order.

8. Record recommendation viewing activities for analytics, personalization, reporting, auditing, recommendation model improvement, and product optimization purposes, where applicable.

9. Ensure that viewing recommendations does not modify any restaurant, menu, food item, pricing, inventory, customer profile, recommendation rules, or configuration master data.

10. Provide a consistent, responsive, and accurate recommendation viewing experience across all supported platforms and devices.

---

#### 3.3.21.12 Failure Response

If the View Recommended Items functionality cannot be completed successfully, the system shall:

1. Inform the customer that recommended food items could not be retrieved.

2. Display an appropriate and user-friendly error message indicating the reason for the failure, where applicable.

3. Display generic recommendations if personalized recommendations cannot be generated and fallback recommendations are available.

4. Display a platform-defined message when no recommendations are available.

5. Allow the customer to retry the recommendation request when the failure is recoverable.

6. Preserve all customer preferences, recommendation data, and recommendation rules without modification.

7. Record recommendation retrieval failures for system monitoring, diagnostics, auditing, analytics, and security purposes, where applicable.

8. Ensure that no restaurant, menu, food item, pricing, inventory, customer profile, recommendation rules, or configuration master data is modified as a result of the failed request.

9. Maintain the customer's current application state and authenticated session unless termination is required due to platform security or system policies.

---

#### 3.3.21.13 Acceptance Criteria

The View Recommended Items functionality shall be considered successfully implemented when all the following conditions are satisfied:

| AC ID | Acceptance Criteria |
|-------|----------------------|
| AC-VRI-001 | The system shall display recommended food items generated by the recommendation engine. |
| AC-VRI-002 | Personalized recommendations shall be displayed for authenticated customers whenever sufficient recommendation data is available. |
| AC-VRI-003 | Generic recommendations shall be displayed when personalized recommendations are unavailable or when the customer is a guest. |
| AC-VRI-004 | The system shall display only active, published, and eligible food items. |
| AC-VRI-005 | The system shall display the latest restaurant information, food item details, pricing, ratings, availability, delivery eligibility, and applicable promotional information. |
| AC-VRI-006 | The system shall clearly identify recommendation labels where applicable. |
| AC-VRI-007 | Customers shall be able to browse and select recommended food items. |
| AC-VRI-008 | Selecting a recommended food item shall open the corresponding food item details page. |
| AC-VRI-009 | The customer shall be able to continue with customization, adding the item to the cart, marking it as a favorite, or placing an order. |
| AC-VRI-010 | The system shall display a platform-defined message when no recommendations are available. |
| AC-VRI-011 | The system shall exclude or appropriately identify unavailable, unpublished, inactive, restricted, or ineligible food items. |
| AC-VRI-012 | Viewing recommended items shall not modify any restaurant, menu, food item, pricing, inventory, customer profile, recommendation rules, or configuration master data. |
| AC-VRI-013 | Recommendation viewing activities shall be recorded for analytics, reporting, auditing, personalization, recommendation model improvement, and product optimization purposes, where applicable. |
| AC-VRI-014 | Appropriate validation and error messages shall be displayed whenever recommendation retrieval cannot be completed successfully. |
| AC-VRI-015 | The system shall provide a consistent, accurate, secure, and responsive recommendation viewing experience across all supported platforms and devices. |
| AC-VRI-016 | The recommendation process shall comply with applicable privacy, security, accessibility, and data protection requirements. |


### 3.3.22 View Popular Items

#### 3.3.22.1 Description

This use case allows customers to view food items that are identified as popular on the QuickBite platform. The system shall retrieve and display popular food items based on platform-defined popularity metrics such as order volume, customer ratings, customer preferences, purchase frequency, customer engagement, restaurant performance, and other business rules. The Popular Items section shall help customers discover frequently ordered and highly preferred food items without modifying any restaurant, menu, food item, pricing, inventory, popularity metrics, customer profile, or configuration master data.

#### 3.3.22.2 Actors

**Primary:**

- Customer

**Supporting:**

- Popularity Service
- Menu Service
- Restaurant Service
- Pricing Service
- Inventory Service
- Customer Profile Service
- Analytics Service
- Authentication and Authorization Service

#### 3.3.22.3 Preconditions

1. The QuickBite platform shall be available.

2. The Popularity Service shall be operational.

3. The required menu, restaurant, pricing, inventory, and popularity data shall be available.

4. The customer may be authenticated or accessing the platform as a guest, subject to platform configuration.

5. Platform-defined popularity metrics shall be available for generating popular food items.

6. The customer accesses a page or section that displays popular food items.

7. All dependent services required for retrieving popular food items shall be operational.

#### 3.3.22.4 Trigger

The customer opens a page or section that displays Popular Items, or the system automatically loads popular food items during customer interaction.

#### 3.3.22.5 Input Fields

| Field | Description | Mandatory |
|-------|-------------|-----------|
| Customer ID | Unique customer identifier (Authenticated customer) | No |
| Session ID | Guest session identifier | No |
| Current Location | Customer delivery location | No |
| Restaurant ID | Restaurant context | No |
| Cuisine Type | Cuisine preference filter | No |
| Page Number | Pagination number | No |
| Page Size | Number of records per page | No |
| Device Information | Device details for analytics | No |
| Popularity Category | Trending, Most Ordered, Highest Rated, etc. | No |


#### 3.3.22.6 Business Rules

1. The system shall display food items identified as popular based on platform-defined popularity criteria.

2. Popular food items shall be determined using one or more of the following metrics, where applicable:
   - Order Volume
   - Purchase Frequency
   - Customer Ratings
   - Customer Reviews
   - Number of Customers Ordering
   - Restaurant Performance
   - Customer Engagement
   - Trending Activity
   - Business Promotion Rules
   - Platform Analytics

3. The popularity calculation shall be managed by the platform and may be updated periodically based on the latest business data.

4. The system shall display only active, published, and orderable food items.

5. The system shall display the latest restaurant information, food item details, pricing, ratings, availability, and applicable promotional information.

6. The system shall not display food items belonging to restaurants that are inactive, unpublished, permanently closed, or restricted.

7. Where location-based filtering is supported, the system shall display only food items that can be delivered to the customer's selected delivery location.

8. The system may categorize popular food items into platform-defined sections such as:
   - Most Ordered
   - Trending
   - Best Sellers
   - Highest Rated
   - Customer Favorites
   - Popular Near You

9. The customer shall be able to browse and select any displayed popular food item.

10. Selecting a popular food item shall navigate the customer to the corresponding food item details page.

11. Viewing popular food items shall not automatically add any item to the cart, favorites, or order history.

12. Viewing popular food items shall not modify any restaurant, menu, food item, pricing, inventory, popularity metrics, customer profile, or configuration master data.

13. The system shall record Popular Items viewing activities for analytics, reporting, auditing, recommendation improvement, customer behavior analysis, and product optimization purposes, where applicable.

14. The Popular Items functionality shall comply with applicable privacy, accessibility, security, and data protection requirements.

#### 3.3.22.7 Validations

1. The system shall validate that the Popularity Service is available before processing the request.

2. The system shall validate that the required popularity metrics are available before retrieving popular food items.

3. The system shall validate that all displayed food items are active, published, and available for ordering.

4. The system shall validate that associated restaurants are active, operational, and eligible to accept customer orders.

5. The system shall validate the latest pricing, inventory, ratings, and availability information before displaying popular food items.

6. The system shall validate the customer's delivery location before displaying location-specific popular food items, where applicable.

7. The system shall validate the requested popularity category against the supported platform-defined categories.

8. The system shall validate pagination parameters when paginated results are requested.

9. The system shall validate that duplicate food items are not displayed within the same Popular Items listing unless permitted by business rules.

10. The system shall validate that incomplete, corrupted, unpublished, deleted, inactive, or restricted food item records are excluded from the displayed results.

11. The system shall validate that popularity information has been successfully retrieved before displaying the Popular Items section.

12. The system shall validate that viewing Popular Items does not modify any restaurant, menu, food item, pricing, inventory, popularity metrics, customer profile, or configuration master data.

13. The system shall display a platform-defined message when no popular food items are available.

14. The system shall display an appropriate validation or error message whenever the Popular Items retrieval request cannot be completed successfully.

#### 3.3.22.8 Main Flow

1. The customer navigates to a page or section that displays **Popular Items**.

2. The system validates the request and verifies the availability of the Popularity Service.

3. The system retrieves the platform-defined popularity data.

4. The system retrieves food items that satisfy the configured popularity criteria.

5. The system retrieves the latest restaurant information, food item details, pricing, ratings, availability, delivery eligibility, and applicable promotional information for each popular food item.

6. The system validates that each food item and its associated restaurant are active, published, and eligible for customer ordering.

7. The system filters out unavailable, unpublished, inactive, deleted, restricted, or ineligible food items.

8. Where applicable, the system filters food items based on the customer's selected delivery location.

9. The system categorizes popular food items according to platform-defined categories, where applicable.

10. The system displays the Popular Items section.

11. For each popular food item, the system displays applicable information, including:
    - Food Item Name
    - Restaurant Name
    - Food Image
    - Current Price
    - Customer Rating
    - Availability Status
    - Delivery Availability
    - Applicable Offers or Discounts
    - Popularity Label (e.g., Most Ordered, Trending, Best Seller, Highest Rated, Popular Near You)

12. The customer browses the displayed popular food items.

13. The customer selects a popular food item.

14. The system opens the selected food item's details page.

15. The customer may continue to customize the food item, add it to the cart, mark it as a favorite, or place an order.

16. The system records Popular Items viewing activities for analytics, reporting, auditing, customer behavior analysis, recommendation improvement, and product optimization purposes, where applicable.

17. The use case ends successfully.

---

#### 3.3.22.9 Alternate Flows

##### AF-1: No Popular Food Items Available

1. The customer opens the Popular Items section.
2. The system determines that no popular food items are currently available.
3. The system displays a platform-defined message indicating that no popular items are available.
4. The use case ends.

---

##### AF-2: Customer Location Is Unavailable

1. The system is unable to determine the customer's delivery location.
2. The system displays platform-wide popular food items instead of location-specific popular items.
3. The use case continues.

---

##### AF-3: Food Item Is No Longer Available

1. During retrieval, the system determines that one or more popular food items are unavailable, unpublished, inactive, deleted, or restricted.
2. The system excludes the affected food items or clearly indicates their availability status according to platform configuration.
3. The remaining valid popular food items are displayed.
4. The use case continues.

---

##### AF-4: Restaurant Cannot Deliver to Customer Location

1. The system determines that one or more restaurants cannot deliver to the customer's selected delivery location.
2. The system excludes those food items or clearly indicates delivery unavailability, according to platform configuration.
3. The remaining eligible popular food items are displayed.
4. The use case continues.

---

##### AF-5: Popularity Data Is Unavailable

1. The system is unable to retrieve the latest popularity metrics.
2. The system displays an appropriate error message.
3. The customer may retry the request later.
4. The use case ends.

---

##### AF-6: Popularity Service Is Unavailable

1. The customer requests the Popular Items section.
2. The Popularity Service is temporarily unavailable.
3. The system displays an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

---

##### AF-7: Popular Items Retrieval Fails

1. The system encounters an unexpected processing, database, network, or service error while retrieving popular food items.
2. The system logs the failure.
3. The system displays an appropriate error message.
4. The customer may retry the request.
5. The use case ends.

### 3.3.23 View Combo Meals

#### 3.3.23.1 Description

This use case allows customers to view combo meals available on the QuickBite platform. The system shall retrieve and display predefined meal combinations offered by restaurants, including the combo name, included food items, pricing, discounts, availability, restaurant information, nutritional information, and applicable promotional offers. The Combo Meals section shall enable customers to discover bundled meal options that provide convenience and value without modifying any restaurant, menu, combo meal, food item, pricing, inventory, promotional configuration, customer profile, or configuration master data.

#### 3.3.23.2 Actors

**Primary:**

- Customer

**Supporting:**

- Combo Meal Service
- Menu Service
- Restaurant Service
- Pricing Service
- Inventory Service
- Promotion Service
- Customer Profile Service
- Authentication and Authorization Service

#### 3.3.23.3 Preconditions

1. The QuickBite platform shall be available.

2. The Combo Meal Service shall be operational.

3. Combo meal information shall be available.

4. The associated restaurants shall be active and operational.

5. The required menu, pricing, inventory, and promotional data shall be available.

6. The customer may be authenticated or accessing the platform as a guest, subject to platform configuration.

7. The customer accesses a page or section that displays combo meals.

8. All dependent services required for retrieving combo meal information shall be operational.

#### 3.3.23.4 Trigger

The customer opens the Combo Meals section or navigates to a page where combo meals are displayed.

#### 3.3.23.5 Input Fields

| Field | Description | Mandatory |
|-------|-------------|-----------|
| Customer ID | Unique customer identifier (Authenticated customer) | No |
| Session ID | Guest session identifier | No |
| Current Location | Customer delivery location | No |
| Restaurant ID | Restaurant context | No |
| Combo Category | Breakfast, Lunch, Dinner, Family Pack, etc. | No |
| Cuisine Type | Cuisine preference filter | No |
| Page Number | Pagination number | No |
| Page Size | Number of records per page | No |
| Device Information | Device details for analytics | No |

#### 3.3.23.6 Business Rules

1. The system shall display only predefined combo meals configured by restaurants.

2. Each combo meal shall consist of one or more food items defined by the restaurant.

3. The system shall display the latest combo meal information, including combo name, included food items, pricing, discounts, availability, and applicable promotional offers.

4. The system shall calculate and display the current combo meal price in accordance with the restaurant's pricing and promotional policies.

5. The system shall display any savings or discounts associated with purchasing the combo meal, where applicable.

6. The system shall display only combo meals that are active, published, and available for ordering.

7. The system shall not display combo meals belonging to restaurants that are inactive, unpublished, permanently closed, or restricted.

8. Where location-based filtering is supported, the system shall display only combo meals available for delivery to the customer's selected delivery location.

9. The system may categorize combo meals into platform-defined categories such as:
   - Breakfast Combos
   - Lunch Combos
   - Dinner Combos
   - Family Meals
   - Party Packs
   - Value Meals
   - Kids Meals
   - Limited-Time Combos

10. The customer shall be able to browse and select any displayed combo meal.

11. Selecting a combo meal shall navigate the customer to the corresponding combo meal details page.

12. Viewing combo meals shall not automatically add any combo meal or its constituent food items to the cart, favorites, or order history.

13. Viewing combo meals shall not modify any restaurant, menu, combo meal, food item, pricing, inventory, promotional configuration, customer profile, or configuration master data.

14. The system shall record Combo Meals viewing activities for analytics, reporting, auditing, customer behavior analysis, recommendation improvement, and product optimization purposes, where applicable.

15. The Combo Meals functionality shall comply with applicable privacy, accessibility, security, and data protection requirements.

#### 3.3.23.7 Validations

1. The system shall validate that the Combo Meal Service is available before processing the request.

2. The system shall validate that combo meal information is available before retrieving combo meal records.

3. The system shall validate that each combo meal is active, published, and eligible for customer viewing.

4. The system shall validate that the associated restaurant is active, operational, and eligible to accept customer orders.

5. The system shall validate that all food items included in the combo meal satisfy the platform-defined availability rules.

6. The system shall validate the latest pricing, discounts, promotional offers, inventory, and availability information before displaying combo meals.

7. The system shall validate the customer's delivery location before displaying location-specific combo meals, where applicable.

8. The system shall validate the requested combo meal category against the supported platform-defined categories.

9. The system shall validate pagination parameters when paginated combo meal results are requested.

10. The system shall validate that duplicate combo meal records are not displayed within the same listing unless permitted by business rules.

11. The system shall validate that incomplete, unpublished, inactive, deleted, expired, restricted, or corrupted combo meal records are excluded from the displayed results.

12. The system shall validate that all displayed promotional offers associated with combo meals are currently active and applicable.

13. The system shall validate that viewing combo meals does not modify any restaurant, menu, combo meal, food item, pricing, inventory, promotional configuration, customer profile, or configuration master data.

14. The system shall display a platform-defined message when no combo meals are available.

15. The system shall display an appropriate validation or error message whenever the Combo Meals retrieval request cannot be completed successfully.

#### 3.3.23.8 Main Flow

1. The customer navigates to the **Combo Meals** section of the QuickBite platform.

2. The system validates the request and verifies the availability of the Combo Meal Service.

3. The system retrieves all available combo meals that satisfy the configured business rules.

4. The system retrieves the latest combo meal information, restaurant information, pricing, discounts, inventory, availability, and applicable promotional offers.

5. The system validates that each combo meal and its associated restaurant are active, published, and eligible for customer ordering.

6. The system validates that all constituent food items included in each combo meal are available.

7. The system filters out unavailable, unpublished, inactive, expired, deleted, restricted, or ineligible combo meals.

8. Where applicable, the system filters combo meals based on the customer's selected delivery location.

9. The system categorizes combo meals according to platform-defined categories, where applicable.

10. The system displays the Combo Meals section.

11. For each combo meal, the system displays applicable information, including:
    - Combo Meal Name
    - Restaurant Name
    - Combo Image
    - Included Food Items
    - Current Combo Price
    - Discount or Savings
    - Customer Rating
    - Availability Status
    - Delivery Availability
    - Applicable Promotional Offers
    - Combo Category

12. The customer browses the available combo meals.

13. The customer selects a combo meal.

14. The system opens the selected combo meal details page.

15. The customer may continue to review the combo contents, customize eligible items (where supported), add the combo meal to the cart, mark it as a favorite, or place an order.

16. The system records Combo Meals viewing activities for analytics, reporting, auditing, customer behavior analysis, recommendation improvement, and product optimization purposes, where applicable.

17. The use case ends successfully.

---

#### 3.3.23.9 Alternate Flows

##### AF-1: No Combo Meals Available

1. The customer opens the Combo Meals section.
2. The system determines that no combo meals are currently available.
3. The system displays a platform-defined message indicating that no combo meals are available.
4. The use case ends.

---

##### AF-2: Customer Location Is Unavailable

1. The system is unable to determine the customer's delivery location.
2. The system displays platform-wide available combo meals instead of location-specific combo meals.
3. The use case continues.

---

##### AF-3: Combo Meal Is No Longer Available

1. During retrieval, the system determines that one or more combo meals are unavailable, unpublished, inactive, expired, deleted, or restricted.
2. The system excludes the affected combo meals or clearly indicates their availability status according to platform configuration.
3. The remaining eligible combo meals are displayed.
4. The use case continues.

---

##### AF-4: Restaurant Cannot Deliver to Customer Location

1. The system determines that one or more restaurants offering combo meals cannot deliver to the customer's selected delivery location.
2. The system excludes those combo meals or clearly indicates delivery unavailability according to platform configuration.
3. The remaining eligible combo meals are displayed.
4. The use case continues.

---

##### AF-5: One or More Combo Items Are Unavailable

1. The system determines that one or more food items included in a combo meal are temporarily unavailable.
2. The system evaluates the combo meal according to platform-defined business rules.
3. If the combo meal remains orderable, the system displays the updated availability information.
4. Otherwise, the system excludes the combo meal from the displayed results.
5. The use case continues.

---

##### AF-6: Combo Meal Service Is Unavailable

1. The customer requests the Combo Meals section.
2. The Combo Meal Service is temporarily unavailable.
3. The system displays an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

---

##### AF-7: Combo Meals Retrieval Fails

1. The system encounters an unexpected processing, database, network, or service error while retrieving combo meals.
2. The system logs the failure.
3. The system displays an appropriate error message.
4. The customer may retry the request.
5. The use case ends.

#### 3.3.23.10 Postconditions

Upon completion of the View Combo Meals functionality, one of the following postconditions shall apply:

##### Successful Completion

1. The available combo meals shall be successfully retrieved and displayed to the customer.

2. The displayed combo meals shall include the latest restaurant information, included food items, pricing, discounts, availability, delivery eligibility, and applicable promotional offers.

3. The customer shall be able to browse and view available combo meals.

4. The customer shall be able to select a combo meal and navigate to its detailed information page.

5. The customer shall be able to continue with applicable actions such as reviewing combo contents, customizing eligible items, adding the combo meal to the cart, marking it as a favorite, or placing an order.

6. Combo Meals viewing activities shall be recorded for analytics, reporting, auditing, customer behavior analysis, recommendation improvement, and product optimization purposes, where applicable.

7. Viewing combo meals shall not modify any restaurant, menu, combo meal, food item, pricing, inventory, promotional configuration, customer profile, or configuration master data.

##### Unsuccessful Completion

1. Combo meals shall not be displayed.

2. The system shall notify the customer that combo meal information could not be retrieved.

3. Existing combo meal definitions, pricing, promotional configurations, and customer information shall remain unchanged.

4. No restaurant, menu, combo meal, food item, pricing, inventory, promotional configuration, customer profile, or configuration master data shall be modified as a result of the failed retrieval request.

5. The customer's authenticated session shall remain active unless termination is required by platform security or system policies.

---

#### 3.3.23.11 Success Response

Upon successful completion of the View Combo Meals functionality, the system shall:

1. Display all eligible combo meals available to the customer.

2. Display the latest combo meal information, restaurant details, included food items, pricing, discounts, availability, delivery eligibility, and applicable promotional offers.

3. Display the savings associated with purchasing the combo meal, where applicable.

4. Display only active, published, and orderable combo meals.

5. Allow the customer to browse and select any displayed combo meal.

6. Navigate the customer to the selected combo meal details page.

7. Allow the customer to review combo contents, customize eligible items, add the combo meal to the cart, mark it as a favorite, or place an order, where applicable.

8. Record Combo Meals viewing activities for analytics, reporting, auditing, customer behavior analysis, recommendation improvement, and product optimization purposes.

9. Ensure that viewing combo meals does not modify any restaurant, menu, combo meal, food item, pricing, inventory, promotional configuration, customer profile, or configuration master data.

10. Provide a consistent, accurate, secure, and responsive combo meal viewing experience across all supported platforms and devices.

---

#### 3.3.23.12 Failure Response

If the View Combo Meals functionality cannot be completed successfully, the system shall:

1. Inform the customer that combo meal information could not be retrieved.

2. Display an appropriate and user-friendly error message indicating the reason for the failure, where applicable.

3. Display a platform-defined message when no combo meals are available.

4. Allow the customer to retry the request when the failure is recoverable.

5. Preserve all combo meal definitions, pricing information, promotional configurations, customer information, and business rules without modification.

6. Record combo meal retrieval failures for system monitoring, diagnostics, auditing, analytics, and security purposes, where applicable.

7. Ensure that no restaurant, menu, combo meal, food item, pricing, inventory, promotional configuration, customer profile, or configuration master data is modified as a result of the failed request.

8. Maintain the customer's authenticated session and current application state unless termination is required due to platform security or system policies.

---

#### 3.3.23.13 Acceptance Criteria

The View Combo Meals functionality shall be considered successfully implemented when all the following conditions are satisfied:

| AC ID | Acceptance Criteria |
|-------|----------------------|
| AC-VCM-001 | The system shall display only active, published, and eligible combo meals. |
| AC-VCM-002 | The system shall display the latest combo meal information, restaurant details, included food items, pricing, discounts, availability, delivery eligibility, and promotional offers. |
| AC-VCM-003 | The system shall accurately calculate and display the current combo meal price and applicable savings. |
| AC-VCM-004 | Only restaurants eligible to receive customer orders shall have their combo meals displayed. |
| AC-VCM-005 | Location-based filtering shall display only combo meals deliverable to the customer's selected location, where applicable. |
| AC-VCM-006 | Customers shall be able to browse and select available combo meals. |
| AC-VCM-007 | Selecting a combo meal shall open the corresponding combo meal details page. |
| AC-VCM-008 | Customers shall be able to review combo contents, customize eligible items, add the combo meal to the cart, mark it as a favorite, or place an order, where supported. |
| AC-VCM-009 | The system shall display a platform-defined message when no combo meals are available. |
| AC-VCM-010 | The system shall exclude or appropriately identify unavailable, unpublished, inactive, expired, deleted, restricted, or ineligible combo meals. |
| AC-VCM-011 | Viewing combo meals shall not modify any restaurant, menu, combo meal, food item, pricing, inventory, promotional configuration, customer profile, or configuration master data. |
| AC-VCM-012 | Combo Meals viewing activities shall be recorded for analytics, reporting, auditing, customer behavior analysis, recommendation improvement, and product optimization purposes. |
| AC-VCM-013 | Appropriate validation and error messages shall be displayed whenever combo meal retrieval cannot be completed successfully. |
| AC-VCM-014 | The system shall provide a consistent, accurate, secure, and responsive combo meal viewing experience across all supported platforms and devices. |
| AC-VCM-015 | The Combo Meals functionality shall comply with applicable privacy, security, accessibility, and data protection requirements. |


### 3.3.24 View Item Availability

#### 3.3.24.1 Description

This use case allows customers to view the real-time availability status of a food item before placing an order. The system shall retrieve and display the latest availability information based on restaurant operating status, inventory, item availability, delivery serviceability, scheduling rules, and other applicable business constraints. The Item Availability functionality shall help customers determine whether a food item is currently available for ordering without modifying any restaurant, menu, food item, inventory, pricing, customer profile, or configuration master data.

#### 3.3.24.2 Actors

**Primary:**

- Customer

**Supporting:**

- Menu Service
- Inventory Service
- Restaurant Service
- Pricing Service
- Delivery Service
- Location Service
- Authentication and Authorization Service

#### 3.3.24.3 Preconditions

1. The QuickBite platform shall be available.

2. The requested food item shall exist in the system.

3. The associated restaurant shall exist.

4. The Menu Service shall be operational.

5. The Inventory Service shall be operational.

6. The Restaurant Service shall be operational.

7. The Delivery Service shall be operational, where delivery availability is applicable.

8. The required inventory, restaurant, menu, and delivery information shall be available.

9. The customer may be authenticated or accessing the platform as a guest, subject to platform configuration.

10. The customer accesses a food item details page or another page displaying item availability.

#### 3.3.24.4 Trigger

The customer opens a food item details page or requests to view the availability status of a food item.

#### 3.3.24.5 Input Fields

| Field | Description | Mandatory |
|-------|-------------|-----------|
| Food Item ID | Unique identifier of the food item | Yes |
| Restaurant ID | Unique identifier of the restaurant | Yes |
| Customer Location | Delivery location for availability verification | No |
| Customer ID | Authenticated customer identifier | No |
| Session ID | Guest session identifier | No |
| Delivery Type | Delivery or Pickup | No |
| Scheduled Order Time | Future delivery or pickup time | No |
| Device Information | Device details for analytics | No |

#### 3.3.24.6 Business Rules

1. The system shall display the current availability status of the selected food item.

2. The availability status shall be determined based on one or more of the following factors:
   - Restaurant Operating Status
   - Food Item Availability
   - Inventory Availability
   - Delivery Serviceability
   - Pickup Availability
   - Business Hours
   - Scheduled Ordering Rules
   - Platform Business Rules

3. The system shall display only the latest availability information retrieved from the platform.

4. The system shall indicate whether the food item is:
   - Available
   - Temporarily Unavailable
   - Out of Stock
   - Not Available for Delivery
   - Available for Pickup Only
   - Available for Scheduled Orders
   - Permanently Unavailable

5. If the restaurant is closed, the system shall clearly indicate that the food item cannot currently be ordered.

6. If inventory is insufficient, the system shall indicate that the food item is currently unavailable or out of stock.

7. Where applicable, availability shall be evaluated based on the customer's selected delivery location.

8. Scheduled order availability shall be determined according to the restaurant's configured operating hours and scheduling policies.

9. The system shall display the latest applicable pricing together with the availability information.

10. The customer shall be able to continue viewing the food item details regardless of its ordering availability.

11. Viewing item availability shall not reserve inventory or temporarily block stock quantities.

12. Viewing item availability shall not modify any restaurant, menu, food item, inventory, pricing, customer profile, delivery configuration, or configuration master data.

13. The system shall record item availability viewing activities for analytics, reporting, auditing, customer behavior analysis, demand forecasting, inventory planning, and product optimization purposes, where applicable.

14. The Item Availability functionality shall comply with applicable privacy, accessibility, security, and data protection requirements.

#### 3.3.24.7 Validations

1. The system shall validate that the specified food item exists.

2. The system shall validate that the associated restaurant exists and is active.

3. The system shall validate that the Menu Service, Inventory Service, and Restaurant Service are available before retrieving availability information.

4. The system shall validate that the food item is active, published, and eligible for customer viewing.

5. The system shall validate the latest inventory status before displaying the availability of the food item.

6. The system shall validate the restaurant's current operating status and business hours.

7. The system shall validate the customer's selected delivery location before determining delivery availability, where applicable.

8. The system shall validate the selected delivery type against the restaurant's supported fulfillment options.

9. The system shall validate the scheduled order time against the restaurant's scheduling policies and operating hours, where applicable.

10. The system shall validate that the latest pricing and availability information has been successfully retrieved before displaying the results.

11. The system shall validate that incomplete, unpublished, inactive, deleted, or restricted food items are not displayed as available for ordering.

12. The system shall validate that viewing item availability does not reserve inventory or modify any restaurant, menu, food item, inventory, pricing, customer profile, delivery configuration, or configuration master data.

13. The system shall display an appropriate status message when the selected food item is unavailable, out of stock, or cannot be delivered.

14. The system shall display an appropriate validation or error message whenever the item availability request cannot be completed successfully.

#### 3.3.24.8 Main Flow

1. The customer navigates to a food item details page or another page displaying item availability.

2. The system validates the request and verifies the availability of the required services.

3. The system retrieves the latest food item information.

4. The system retrieves the associated restaurant information.

5. The system retrieves the latest inventory status for the selected food item.

6. The system verifies the restaurant's current operating status and business hours.

7. Where applicable, the system validates the customer's selected delivery location and delivery type.

8. Where applicable, the system validates the scheduled order time against the restaurant's scheduling policies.

9. The system determines the current availability status of the food item based on configured business rules.

10. The system retrieves the latest pricing and applicable promotional information.

11. The system displays the food item together with its availability information, including:
    - Food Item Name
    - Restaurant Name
    - Current Price
    - Availability Status
    - Inventory Status
    - Restaurant Status
    - Delivery Availability
    - Pickup Availability
    - Scheduled Order Availability
    - Applicable Availability Messages

12. The customer reviews the displayed availability information.

13. If the food item is available, the customer may continue to customize the item, add it to the cart, or place an order.

14. If the food item is unavailable, the customer may continue browsing the menu or select an alternative food item.

15. The system records Item Availability viewing activities for analytics, reporting, auditing, customer behavior analysis, demand forecasting, inventory planning, and product optimization purposes, where applicable.

16. The use case ends successfully.

---

#### 3.3.24.9 Alternate Flows

##### AF-1: Restaurant Is Currently Closed

1. The system determines that the associated restaurant is currently closed.
2. The system displays the restaurant status and indicates that the food item cannot currently be ordered.
3. If scheduled ordering is supported, the system displays the next available ordering time.
4. The use case continues.

---

##### AF-2: Food Item Is Out of Stock

1. The system determines that the selected food item is out of stock.
2. The system displays an appropriate availability message.
3. The customer may continue browsing the menu or select another food item.
4. The use case continues.

---

##### AF-3: Food Item Is Temporarily Unavailable

1. The system determines that the food item is temporarily unavailable due to operational or inventory constraints.
2. The system displays an appropriate availability message.
3. The customer may browse alternative food items.
4. The use case continues.

---

##### AF-4: Delivery Is Not Available

1. The system determines that the restaurant cannot deliver to the customer's selected delivery location.
2. The system indicates that delivery is unavailable.
3. If pickup is supported, the system displays pickup availability.
4. The use case continues.

---

##### AF-5: Scheduled Order Is Not Supported

1. The customer requests availability for a scheduled order.
2. The system determines that the selected scheduled time does not satisfy the restaurant's scheduling rules.
3. The system displays an appropriate validation message.
4. The customer may select another scheduled time or place an immediate order, where applicable.
5. The use case continues.

---

##### AF-6: Inventory Information Cannot Be Retrieved

1. The system is unable to retrieve the latest inventory information.
2. The system displays an appropriate error message.
3. The customer may retry the request later.
4. The use case ends.

---

##### AF-7: Item Availability Retrieval Fails

1. The system encounters an unexpected processing, database, network, or service error while retrieving availability information.
2. The system logs the failure.
3. The system displays an appropriate error message.
4. The customer may retry the request.
5. The use case ends.

#### 3.3.24.10 Postconditions

Upon completion of the View Item Availability functionality, one of the following postconditions shall apply:

##### Successful Completion

1. The latest availability status of the selected food item shall be successfully retrieved and displayed.

2. The displayed availability information shall include the latest restaurant status, inventory status, pricing, delivery eligibility, pickup availability, and scheduled ordering availability, where applicable.

3. The customer shall be able to determine whether the selected food item is currently available for ordering.

4. If the food item is available, the customer shall be able to continue with applicable actions such as customization, adding the item to the cart, or placing an order.

5. If the food item is unavailable, the customer shall be informed of the applicable availability reason and may continue browsing alternative food items.

6. Item Availability viewing activities shall be recorded for analytics, reporting, auditing, customer behavior analysis, demand forecasting, inventory planning, and product optimization purposes, where applicable.

7. Viewing item availability shall not reserve inventory or modify any restaurant, menu, food item, inventory, pricing, customer profile, delivery configuration, or configuration master data.

##### Unsuccessful Completion

1. The food item's availability information shall not be displayed.

2. The system shall notify the customer that the availability information could not be retrieved.

3. Existing inventory records, restaurant information, pricing information, and delivery configurations shall remain unchanged.

4. No restaurant, menu, food item, inventory, pricing, customer profile, delivery configuration, or configuration master data shall be modified as a result of the failed availability retrieval request.

5. The customer's authenticated session shall remain active unless termination is required by platform security or system policies.

---

#### 3.3.24.11 Success Response

Upon successful completion of the View Item Availability functionality, the system shall:

1. Display the latest availability status of the selected food item.

2. Display the latest restaurant status, inventory status, pricing, delivery eligibility, pickup availability, and scheduled ordering availability, where applicable.

3. Clearly indicate whether the food item is:
   - Available
   - Temporarily Unavailable
   - Out of Stock
   - Available for Pickup Only
   - Available for Scheduled Orders
   - Not Deliverable
   - Permanently Unavailable

4. Allow the customer to continue viewing the food item details.

5. Allow the customer to proceed with customization, adding the item to the cart, or placing an order when the food item is available.

6. Display appropriate availability messages whenever ordering restrictions apply.

7. Record Item Availability viewing activities for analytics, reporting, auditing, customer behavior analysis, demand forecasting, inventory planning, and product optimization purposes.

8. Ensure that viewing item availability does not reserve inventory or modify any restaurant, menu, food item, inventory, pricing, customer profile, delivery configuration, or configuration master data.

9. Provide a consistent, accurate, secure, and responsive availability viewing experience across all supported platforms and devices.

---

#### 3.3.24.12 Failure Response

If the View Item Availability functionality cannot be completed successfully, the system shall:

1. Inform the customer that the food item's availability information could not be retrieved.

2. Display an appropriate and user-friendly error message indicating the reason for the failure, where applicable.

3. Display an appropriate status message when the food item is unavailable, out of stock, temporarily unavailable, or cannot be delivered.

4. Allow the customer to retry the availability request when the failure is recoverable.

5. Preserve all inventory records, restaurant information, pricing information, delivery configurations, and business rules without modification.

6. Record availability retrieval failures for system monitoring, diagnostics, auditing, analytics, and security purposes, where applicable.

7. Ensure that no restaurant, menu, food item, inventory, pricing, customer profile, delivery configuration, or configuration master data is modified as a result of the failed request.

8. Maintain the customer's authenticated session and current application state unless termination is required due to platform security or system policies.

---

#### 3.3.24.13 Acceptance Criteria

The View Item Availability functionality shall be considered successfully implemented when all the following conditions are satisfied:

| AC ID | Acceptance Criteria |
|-------|----------------------|
| AC-VIA-001 | The system shall display the latest availability status of the selected food item. |
| AC-VIA-002 | The system shall accurately determine availability based on restaurant status, inventory, business hours, delivery eligibility, and platform business rules. |
| AC-VIA-003 | The system shall display the latest restaurant status, inventory status, pricing, delivery availability, pickup availability, and scheduled ordering availability, where applicable. |
| AC-VIA-004 | The system shall clearly indicate the current ordering status of the selected food item. |
| AC-VIA-005 | Customers shall be able to continue viewing the food item details regardless of ordering availability. |
| AC-VIA-006 | Customers shall be able to proceed with customization, adding the item to the cart, or placing an order when the food item is available. |
| AC-VIA-007 | The system shall display appropriate messages when the food item is unavailable, out of stock, temporarily unavailable, or cannot be delivered. |
| AC-VIA-008 | The system shall support delivery, pickup, and scheduled ordering availability checks where applicable. |
| AC-VIA-009 | The system shall not reserve inventory while customers are viewing item availability. |
| AC-VIA-010 | Viewing item availability shall not modify any restaurant, menu, food item, inventory, pricing, customer profile, delivery configuration, or configuration master data. |
| AC-VIA-011 | Item Availability viewing activities shall be recorded for analytics, reporting, auditing, customer behavior analysis, demand forecasting, inventory planning, and product optimization purposes. |
| AC-VIA-012 | Appropriate validation and error messages shall be displayed whenever item availability information cannot be retrieved successfully. |
| AC-VIA-013 | The system shall provide a consistent, accurate, secure, and responsive item availability viewing experience across all supported platforms and devices. |
| AC-VIA-014 | The Item Availability functionality shall comply with applicable privacy, security, accessibility, and data protection requirements. |

### 3.3.25 Share Menu Item

#### 3.3.25.1 Description

This use case allows customers to share a menu item with other users through supported communication channels. The system shall generate a secure shareable link containing the selected food item's information and invoke the device's supported sharing options, such as messaging applications, email, social media platforms, or copy link functionality. Sharing a menu item shall enable customers to recommend food items to others without modifying any restaurant, menu, food item, pricing, inventory, customer profile, order data, or configuration master data.

#### 3.3.25.2 Actors

**Primary:**

- Customer

**Supporting:**

- Menu Service
- Share Service
- Restaurant Service
- Pricing Service
- Deep Link Service
- Notification Service
- Authentication and Authorization Service
- Mobile Operating System / Device Share Framework

#### 3.3.25.3 Preconditions

1. The QuickBite platform shall be available.

2. The selected food item shall exist in the system.

3. The associated restaurant shall exist and be active.

4. The Share Service shall be operational.

5. The Deep Link Service shall be operational.

6. The selected food item shall be eligible for sharing according to platform policies.

7. The customer may be authenticated or accessing the platform as a guest, subject to platform configuration.

8. The customer accesses the food item details page or another page containing the Share option.

9. The customer's device shall support one or more sharing mechanisms.

#### 3.3.25.4 Trigger

The customer selects the **Share** option for a menu item.

#### 3.3.25.5 Input Fields

| Field | Description | Mandatory |
|-------|-------------|-----------|
| Food Item ID | Unique identifier of the selected food item | Yes |
| Restaurant ID | Unique identifier of the restaurant | Yes |
| Customer ID | Authenticated customer identifier | No |
| Session ID | Guest session identifier | No |
| Share Channel | Messaging App, Email, Social Media, Copy Link, etc. | Yes |
| Device Information | Device details for supported sharing options | No |
| Language Preference | Preferred language for shared content | No |
| Referral Code | Customer referral code, where applicable | No |

#### 3.3.25.6 Business Rules

1. The system shall allow customers to share eligible menu items through supported sharing channels.

2. The system shall generate a secure and valid shareable link for the selected menu item.

3. The shared content shall include the latest food item information available at the time of sharing.

4. The shared content may include one or more of the following information, where applicable:
   - Food Item Name
   - Restaurant Name
   - Food Image
   - Current Price
   - Short Description
   - Cuisine Type
   - Deep Link
   - Promotional Information
   - Referral Code
   - Platform Branding

5. The system shall generate deep links that open the corresponding menu item within the QuickBite application whenever supported.

6. If the QuickBite application is not installed, the shared link shall redirect the recipient to the supported web page or application installation page according to platform configuration.

7. The system shall ensure that generated share links are secure and cannot expose confidential customer or platform information.

8. The customer shall be allowed to choose from the supported sharing channels available on the device.

9. The system shall not automatically send shared content without explicit customer confirmation through the selected sharing application.

10. Sharing a menu item shall not create an order, reservation, favorite item, cart item, or notification unless explicitly initiated through another use case.

11. Sharing a menu item shall not modify any restaurant, menu, food item, pricing, inventory, customer profile, order data, or configuration master data.

12. The system shall record menu item sharing activities for analytics, reporting, auditing, customer engagement analysis, marketing effectiveness, referral tracking, and product optimization purposes, where applicable.

13. Referral information shall be included only when the customer is eligible for the referral program and platform policies permit referral sharing.

14. The Share Menu Item functionality shall comply with applicable privacy, accessibility, security, copyright, and data protection requirements.

#### 3.3.25.7 Validations

1. The system shall validate that the selected food item exists.

2. The system shall validate that the associated restaurant exists and is active.

3. The system shall validate that the Share Service and Deep Link Service are available before generating shareable content.

4. The system shall validate that the selected menu item is active, published, and eligible for sharing according to platform policies.

5. The system shall validate that the latest food item information has been successfully retrieved before generating the shared content.

6. The system shall validate the selected sharing channel against the sharing mechanisms supported by the customer's device.

7. The system shall validate the generated share link before presenting it to the customer.

8. The system shall validate that any referral code included in the shared content belongs to the authenticated customer and is currently valid, where applicable.

9. The system shall validate that confidential customer information is excluded from the generated shared content.

10. The system shall validate that expired, unpublished, deleted, inactive, or restricted food items cannot be shared.

11. The system shall validate that generated deep links correctly reference the selected menu item.

12. The system shall validate that sharing a menu item does not create or modify any order, cart item, favorite item, pricing information, inventory, customer profile, or configuration master data.

13. The system shall validate that the sharing request complies with applicable platform security and privacy policies.

14. The system shall display an appropriate validation or error message whenever the share request cannot be completed successfully.

#### 3.3.25.8 Main Flow

1. The customer navigates to a page displaying a menu item.

2. The customer selects the **Share** option for the desired menu item.

3. The system validates the sharing request.

4. The system verifies that the selected menu item is active, published, and eligible for sharing.

5. The system retrieves the latest menu item information.

6. The system retrieves the associated restaurant information.

7. The system generates a secure shareable deep link for the selected menu item.

8. The system prepares the share content using the latest available information.

9. The system displays the device's supported sharing options.

10. The customer selects a preferred sharing channel.

11. The system transfers the prepared share content to the selected sharing application.

12. The selected sharing application displays the generated message for customer review.

13. The customer reviews the shared content.

14. The customer confirms the sharing action within the selected application.

15. The selected sharing application sends the shared content to the intended recipient.

16. The system records the sharing activity for analytics, reporting, auditing, referral tracking, customer engagement analysis, marketing effectiveness, and product optimization purposes, where applicable.

17. The use case ends successfully.

---

#### 3.3.25.9 Alternate Flows

##### AF-1: Selected Menu Item Cannot Be Shared

1. The system determines that the selected menu item is inactive, unpublished, deleted, restricted, or otherwise ineligible for sharing.
2. The system displays an appropriate validation message.
3. The sharing process is terminated.
4. The use case ends.

---

##### AF-2: No Supported Sharing Applications Available

1. The customer selects the Share option.
2. The system determines that no supported sharing applications are available on the customer's device.
3. The system displays an appropriate message.
4. The customer may copy the generated share link if supported.
5. The use case ends.

---

##### AF-3: Customer Selects Copy Link

1. The customer selects the **Copy Link** option.
2. The system copies the generated secure share link to the device clipboard.
3. The system displays a confirmation message indicating that the link has been copied successfully.
4. The customer may paste the link into any supported application.
5. The use case ends successfully.

---

##### AF-4: Customer Cancels Sharing

1. The customer opens the device sharing interface.
2. The customer closes or cancels the sharing process before confirmation.
3. No shared content is transmitted.
4. The system records the cancellation event where applicable.
5. The use case ends.

---

##### AF-5: Share Link Generation Fails

1. The system is unable to generate the secure share link.
2. The system displays an appropriate error message.
3. The customer may retry the sharing request.
4. The use case ends.

---

##### AF-6: Sharing Application Fails

1. The selected sharing application encounters an unexpected failure while processing the shared content.
2. The system displays an appropriate notification, where supported.
3. The customer may retry using the same or another sharing channel.
4. The use case ends.

---

##### AF-7: Share Service Is Unavailable

1. The Share Service or Deep Link Service is temporarily unavailable.
2. The system cannot generate the shareable content.
3. The system displays an appropriate error message.
4. The customer may retry the request later.
5. The use case ends.

#### 3.3.25.10 Postconditions

Upon completion of the Share Menu Item functionality, one of the following postconditions shall apply:

##### Successful Completion

1. A secure shareable link for the selected menu item shall be successfully generated.

2. The selected sharing application shall receive the generated share content.

3. The customer shall have the opportunity to review and confirm the sharing action within the selected sharing application.

4. If the customer confirms the sharing action, the menu item information shall be shared through the selected communication channel.

5. Menu item sharing activities shall be recorded for analytics, reporting, auditing, referral tracking, customer engagement analysis, marketing effectiveness, and product optimization purposes, where applicable.

6. Any applicable referral information shall remain associated with the generated share link according to platform policies.

7. Sharing the menu item shall not modify any restaurant, menu, food item, pricing, inventory, customer profile, order data, or configuration master data.

##### Unsuccessful Completion

1. The menu item shall not be shared.

2. The system shall notify the customer that the sharing request could not be completed.

3. No shareable link shall be distributed if the sharing process fails before customer confirmation.

4. No restaurant, menu, food item, pricing, inventory, customer profile, order data, or configuration master data shall be modified as a result of the failed sharing request.

5. The customer's authenticated session shall remain active unless termination is required by platform security or system policies.

---

#### 3.3.25.11 Success Response

Upon successful completion of the Share Menu Item functionality, the system shall:

1. Generate a secure shareable link for the selected menu item.

2. Display or invoke the device's supported sharing options.

3. Transfer the prepared share content to the selected sharing application.

4. Include the latest menu item information, restaurant information, deep link, and applicable promotional or referral information, where permitted.

5. Allow the customer to review the share content before it is transmitted.

6. Complete the sharing process upon customer confirmation within the selected application.

7. Record sharing activities for analytics, reporting, auditing, referral tracking, customer engagement analysis, marketing effectiveness, and product optimization purposes.

8. Ensure that sharing the menu item does not create or modify any order, cart item, favorite item, pricing information, inventory, customer profile, or configuration master data.

9. Provide a consistent, secure, and responsive sharing experience across all supported platforms and devices.

---

#### 3.3.25.12 Failure Response

If the Share Menu Item functionality cannot be completed successfully, the system shall:

1. Inform the customer that the menu item could not be shared.

2. Display an appropriate and user-friendly error message indicating the reason for the failure, where applicable.

3. Prevent distribution of incomplete or invalid share content.

4. Allow the customer to retry the sharing request when the failure is recoverable.

5. Preserve all restaurant information, menu information, pricing information, inventory information, customer information, and referral data without modification.

6. Record sharing failures for system monitoring, diagnostics, auditing, analytics, and security purposes, where applicable.

7. Ensure that no order, cart item, favorite item, pricing information, inventory, customer profile, or configuration master data is modified as a result of the failed sharing request.

8. Maintain the customer's authenticated session and current application state unless termination is required due to platform security or system policies.

---

#### 3.3.25.13 Acceptance Criteria

The Share Menu Item functionality shall be considered successfully implemented when all the following conditions are satisfied:

| AC ID | Acceptance Criteria |
|-------|----------------------|
| AC-SMI-001 | The system shall allow customers to share eligible menu items through supported sharing channels. |
| AC-SMI-002 | The system shall generate a secure shareable deep link for the selected menu item. |
| AC-SMI-003 | The shared content shall contain the latest menu item information available at the time of sharing. |
| AC-SMI-004 | The system shall invoke the supported device sharing interface. |
| AC-SMI-005 | Customers shall be able to choose any supported sharing channel available on their device. |
| AC-SMI-006 | Customers shall be able to review the share content before confirming the sharing action. |
| AC-SMI-007 | The system shall support Copy Link functionality where available. |
| AC-SMI-008 | Referral information shall be included only when permitted by platform policies. |
| AC-SMI-009 | Sharing shall not automatically create an order, cart item, favorite item, or notification. |
| AC-SMI-010 | Sharing a menu item shall not modify any restaurant, menu, food item, pricing, inventory, customer profile, order data, or configuration master data. |
| AC-SMI-011 | The system shall prevent inactive, unpublished, deleted, or restricted menu items from being shared. |
| AC-SMI-012 | Sharing activities shall be recorded for analytics, reporting, auditing, referral tracking, customer engagement analysis, marketing effectiveness, and product optimization purposes. |
| AC-SMI-013 | Appropriate validation and error messages shall be displayed whenever the sharing request cannot be completed successfully. |
| AC-SMI-014 | The system shall provide a consistent, secure, and responsive sharing experience across all supported platforms and devices. |
| AC-SMI-015 | The Share Menu Item functionality shall comply with applicable privacy, security, accessibility, copyright, and data protection requirements. |

---

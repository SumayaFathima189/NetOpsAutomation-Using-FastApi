# NetOpsAutomation-Using-FastApi
# Introduction
This FastAPI application provides a set of endpoints to interact with the Cisco Firepower Device Manager (FDM) API. It allows you to manage network objects, access policies, port objects, and NAT rules and other network objects.
# Example Usage
To get started, make sure you have the required dependencies installed. You can do this by running:

--->pip install fastapi requests uvicorn

Next, you can start the FastAPI server:

-->uvicorn main:app --reload

# API Endpoints
## Network Objects
Get a list of network objects
### *Method: GET*
Path: /network_objects

Description: Get a list of network objects.

Create a new network object

### *Method: POST*
Path: /create_network_object

Description: Create a new network object.

Request Body: JSON containing network object data.

Delete a network object by its ID

### *Method: DELETE*
Path: /delete_network_object/{object_id}

Description: Delete a network object by its ID.

Update a network object by its ID

### *Method: PUT*
Path: /update_network_object/{object_id}

Description: Update a network object by its ID.

Request Body: JSON containing updated network object data.

## Access Policy
Get a list of access policies

### *Method: GET*
Path: /access_policies

Description: Get a list of access policies.

Get access rules for a specific policy by its ID

### *Method: GET*
Path: /get_access_rules/{policy_id}

Description: Get access rules for a specific policy by its ID.

Create a new access rule for a specific policy

### *Method: POST*
Path: /create_access_rule/{policy_id}

Description: Create a new access rule for a specific policy.

Request Body: JSON containing access rule data.

Delete an access rule by its ID

### *Method: DELETE*
Path: /delete_access_rule/{policy_id}/{rule_id}

Description: Delete an access rule by its ID.

Update an access rule by its ID

### *Method: PUT*
Path: /update_access_rule/{parent_id}/{object_id}

Description: Update an access rule by its ID.

Request Body: JSON containing updated access rule data.

## Port Objects
Get a list of port objects

### *Method: GET*
Path: /get_port_objects/{limit}

Description: Get a list of port objects. You can specify a limit.

Create a new port object

### *Method: POST*
Path: /create_port_object

Description: Create a new port object.

Request Body: JSON containing port object data.

Delete a port object by its ID

### *Method: DELETE*
Path: /delete_port_object/{port_id}

Description: Delete a port object by its ID.

Update a port object by its ID

### *Method: PUT*
Path: /update_port_object/{object_id}

Description: Update a port object by its ID.

Request Body: JSON containing updated port object data.

## NAT Rules
Auto NAT Rules
Get a list of auto NAT rules

### *Method: GET*
Path: /nat_auto_rules

Description: Get a list of auto NAT rules.

Create a new auto NAT rule

### *Method: POST*
Path: /create_nat_auto_rule

Description: Create a new auto NAT rule.

Request Body: JSON containing auto NAT rule data.

Delete an auto NAT rule by its ID

### *Method: DELETE*
Path: /delete_nat_auto_rule/{rule_id}

Description: Delete an auto NAT rule by its ID.

Update an auto NAT rule by its ID

### *Method: PUT*
Path: /update_nat_auto_rule/{rule_id}

Description: Update an auto NAT rule by its ID.

Request Body: JSON containing updated auto NAT rule data.

## Manual NAT Rules
Get a list of manual NAT rules

### *Method: GET*
Path: /nat_manual_rules

Description: Get a list of manual NAT rules.

Create a new manual NAT rule

### *Method: POST*
Path: /create_nat_manual_rule

Description: Create a new manual NAT rule.

Request Body: JSON containing manual NAT rule data.

Delete a manual NAT rule by its ID

### *Method: DELETE*
Path: /delete_nat_manual_rule/{rule_id}

Description: Delete a manual NAT rule by its ID.

Update a manual NAT rule by its ID

### *Method: PUT*
Path: /update_nat_manual_rule/{rule_id}

Description: Update a manual NAT rule by its ID.

Request Body: JSON containing updated manual NAT rule data.

## Function Signatures:
### *get_token*
Description: Retrieves the authentication token from the FDM API.

Signature: get_token(token: str = Depends(get_Token)) -> str

### *get_network*
Description: Retrieves a list of network objects.

Signature: get_network(token: str = Depends(get_token)) -> dict

### *create_network_object*
Description: Creates a network object.

Signature: create_network_object(network_data: dict, token: str = Depends(get_token)) -> dict

### *delete_network_object*
Description: Deletes a network object.

Signature: delete_network_object(object_id: str, token: str = Depends(get_token)) -> dict

### *update_network_object*
Description: Updates a network object.

Signature: update_network_object(object_id: str, network_object_data: dict, token: str = Depends(get_token)) -> dict

### *get_access_policies*
Description: Retrieves a list of access policies.

Signature: get_access_policies(token: str = Depends(get_token)) -> str

### *get_access_rules*
Description: Retrieves access rules for a specific policy.

Signature: get_access_rules(policy_id: str, token: str = Depends(get_token)) -> dict

## Examples
### *Example 1: Retrieving Authentication Token:*
token = get_token()

print(f"Authentication Token: {token}")

### *Example 2: Creating a Network Object:*
network_data = {

"name": "Office_Network",

"subnet": "192.168.1.0/24"
}

response = create_network_object(network_data)

print(f"Created Network Object: {response}")

### *Example 3: Deleting a Network Object:*
object_id = "network_object_id_here"

response = delete_network_object(object_id)

print(response)

### *Example 4: Updating a Network Object:*
object_id = "network_object_id_here"

network_object_data = {

"name": "Updated_Office_Network",

"subnet": "192.168.1.0/24"
}

response = update_network_object(object_id, network_object_data)

print(f"Updated Network Object: {response}")

### *Example 5: Retrieving a List of Access Policies:*
access_policies = get_access_policies()

print(f"Access Policies: {access_policies}")

### *Example 6: Retrieving Access Rules for a Specific Policy:*

policy_id = "policy_id_here"

access_rules = get_access_rules(policy_id)

print(f"Access Rules for Policy {policy_id}: {access_rules}")

### *Example 7: Creating an Access Rule*
policy_id = "policy_id_here"

access_rule_data = {

"name": "Allow_HTTP",

"sourceNetworks": ["192.168.1.0/24"],

"destinationNetworks": ["0.0.0.0/0"],

"services": ["HTTP"],

"action": "ALLOW"
}

response = create_access_rule(policy_id, access_rule_data)

print(f"Created Access Rule: {response}")

### *Example 8: Deleting an Access Rule:*
policy_id = "policy_id_here"

object_id = "access_rule_id_here"

response = delete_access_rule(policy_id, object_id)

print(response)

### *Example 9: Updating an Access Rule:*
parent_id = "policy_id_here"

object_id = "access_rule_id_here"

access_rule_data = {

"name": "Updated_HTTP_Rule",

"sourceNetworks": ["192.168.1.0/24"],

"destinationNetworks": ["0.0.0.0/0"],

"services": ["HTTP"],

"action": "ALLOW"
}

response = update_access_rule(parent_id, object_id, access_rule_data)

print(f"Updated Access Rule: {response}")




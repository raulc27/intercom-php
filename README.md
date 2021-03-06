
[![Code
Climate](https://codeclimate.com/repos/537da4a7e30ba062b101be9c/badges/2aa25d4736f09f40282e/gpa.svg)](https://codeclimate.com/repos/537da4a7e30ba062b101be9c/feed)

[![Build
Status](https://travis-ci.org/intercom/intercom-php.svg?branch=master)](https://travis-ci.org/intercom/intercom-php)

## Installation

Requires PHP 5.6.

Using Composer:

The recommended way to install intercom-php is through [Composer](https://getcomposer.org):

First, install Composer:

```
$ curl -sS https://getcomposer.org/installer | php
```

Next, install the latest intercom-php:

```
$ php composer.phar require intercom/intercom-php
```

Finally, you can include the files in your PHP script:

```php
require "vendor/autoload.php";
```

## Clients
For OAuth or Access Tokens use:

```php
use Intercom\IntercomClient;

$client = new IntercomClient(<insert_token_here>, null);
```
> If you already have an access token you can find it [here](https://app.intercom.com/developers/_). If you want to create or learn more about access tokens then you can find more info [here](https://developers.intercom.io/docs/personal-access-tokens).

If you are building a third party application you can get your OAuth token by [setting-up-oauth](https://developers.intercom.io/page/setting-up-oauth) for Intercom.

## Users

```php
// Create a user
$client->users->create([
  "email" => "test@intercom.io",
  "custom_attributes" => ['foo' => 'bar']
]);

// Update a user (Note: This method is an alias to the create method. In practice you can use create to update users if you wish)
$client->users->update([
  "email" => "test@intercom.io",
  "custom_attributes" => ['foo' => 'bar']
]);

// Delete a user by ID
$client->users->deleteUser("570680a8a1bcbca8a90001b9");

// Get a user by ID
$client->users->getUser("570680a8a1bcbca8a90001b9");

// Add companies to a user
$client->users->create([
  "email" => "test@intercom.io",
  "companies" => [
    [
      "company_id" => "3"
    ]
  ]
]);

// Remove companies from a user
$client->users->create([
  "email" => "test@intercom.io",
  "companies" => [
    [
      "company_id" => "3",
      "remove" => true
    ]
  ]
]);

// Find a single user by email
$client->users->getUsers(["email" => "bob@intercom.io"]);

// List all users
$client->users->getUsers([]);
```

## Leads

```php
// Create a lead
// See more options here: https://developers.intercom.io/reference#create-lead
$client->leads->create([
  "email" => "test@intercom.io",
  "custom_attributes" => ['foo' => 'bar']
]);

// Update a lead (Note: This method is an alias to the create method. In practice you can use create to update leads if you wish)
$client->leads->update([
  "email" => "test@intercom.io",
  "custom_attributes" => ['foo' => 'bar']
]);

// List leads
// See more options here: https://developers.intercom.io/reference#list-leads
$client->leads->getLeads([]);

// Find a lead by ID
$client->leads->getLead("570680a8a1bcbca8a90000a9");

// Delete a lead by ID
$client->leads->deleteLead("570680a8a1bcbca8a90000a9");

// Convert a Lead to a User
$leads->convertLead([
  "contact" => [
    "user_id" => "8a88a590-e1c3-41e2-a502-e0649dbf721c"
  ],
  "user" => [
    "email" => "winstonsmith@truth.org"
  ]
]);
```

## Tags

```php
// List tags
$client->tags->getTags();

// Tag users
// See more options here: https://developers.intercom.io/reference#tag-or-untag-users-companies-leads-contacts
$client->tags->tag([
  "name" => "Test",
  "users" => [
    ["id" => "1234"]
  ]
]);
```

## Segments

```php
// List Segments
$client->segments->getSegments();
```


## Events

```php
// Create an event
$client->events->create([
  "event_name" => "testing",
  "created_at" => 1391691571,
  "email" => "test@intercom.io"
]);

// View events for a user
$client->events->getEvents(["email" => "bob@intercom.io"]);
```

## Companies

```php
// Create a company
$client->companies->create([
  "name" => "foocorp", "company_id" => "3"
]);

// Update a company (Note: This method is an alias to the create method. In practice you can use create to update companies if you wish)
$client->companies->update([
  "name" => "foocorp", "id" => "3"
]);

// List Companies
$client->companies->getCompanies([]);
```

## Admins

```php
// List admins
$client->admins->getAdmins();
```

## Messages

```php
// Send a message from an admin to a user
// See more options here: https://developers.intercom.io/reference#conversations
$client->messages->create([
  "message_type" => "inapp",
  "subject" => "Hey",
  "body" => "Ponies, cute small horses or something more sinister?",
  "from" => [
    "type" => "admin",
    "id" => "1234"
  ],
  "to" => [
    "type" => "user",
    "email" => "bob@intercom.io"
  ]
]);
```

## Conversations

```php
// List conversations for an admin
// See more options here: https://developers.intercom.io/reference#list-conversations
$client->conversations->getConversations([
  "type" => "admin",
  "admin_id" => "25610"
]);

// Get a single conversation
$client->conversations->getConversation("1234")

// Reply to a conversation
// See more options here: https://developers.intercom.io/reference#replying-to-a-conversation
$client->conversations->replyToConversation("5678", [
  "email" => "test@intercom.io",
  "body" => "Thanks :)",
  "type" => "user",
  "message_type" => "comment"
]);

//Reply to a user's last conversation
// See more options here: https://developers.intercom.com/reference#replying-to-users-last-conversation
$client->conversations->replyToLastConversation([
  "email" => "test@intercom.io",
  "body" => "Thanks :)",
  "type" => "user",
  "message_type" => "comment"
]);

// Mark a conversation as read
// See API documentation here: https://developers.intercom.io/reference#marking-a-conversation-as-read
$client->conversations->markConversationAsRead("7890");
```

## Counts

```php
// List counts
// See more options here: https://developers.intercom.io/reference#getting-counts
$client->counts->getCounts([])
```

## Notes

```php
// Create a note
$client->notes->create([
  "admin_id" => "21",
  "body" => "Text for my note",
  "user" => [
    "id" => "5310d8e8598c9a0b24000005"
  ]
]);

// List notes for a user
$client->notes->getNotes([
  "user_id" => "25"
]);

// Get a single Note by id
$client->notes->getNote("42");
```

## Pagination

When listing, the Intercom API may return a pagination object:

```json
{
  "pages": {
    "next": "..."
  }
}
```

You can grab the next page of results using the client:

```php
$client->nextPage($response->pages);
```


## Exceptions

Exceptions are handled by [Guzzle](https://github.com/guzzle/guzzle).
The Intercom API may return an unsuccessful HTTP response, for example when a resource is not found (404).
If you want to catch errors you can wrap your API call into a try/catch:

```php
use GuzzleHttp\Exception\ClientException;

try {
  $user = $client->users->getUser("570680a8a1bcbca8a90001b9");
} catch(ClientException $e) {
  $response = $e->getResponse();
  $statusCode = $response->getStatusCode();
  if ($statusCode == '404') {
    // Handle 404 error
    return;
  } else {
    throw $e;
  }
}
```

## Pull Requests

- **Add tests!** Your patch won't be accepted if it doesn't have tests.

- **Document any change in behaviour**. Make sure the README and any other
  relevant documentation are kept up-to-date.

- **Create topic branches**. Don't ask us to pull from your master branch.

- **One pull request per feature**. If you want to do more than one thing, send
  multiple pull requests.

- **Send coherent history**. Make sure each individual commit in your pull
  request is meaningful. If you had to make multiple intermediate commits while
  developing, please squash them before sending them to us.

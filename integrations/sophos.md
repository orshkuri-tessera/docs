---
title: Sophos Central
description: Prepare a Sophos Central account so Arch can read the computers it protects.
---

## Before you start

You need the Super Admin role in the Sophos Central account that manages your computers. A partner,
organization or distributor credential reaches many accounts, so Arch refuses it.

## Setup steps

1. Sign in to Sophos Central, select Global Settings, go to Access Control and select API Credentials. See
   [API Credentials](https://docs.sophos.com/central/customer/help/en-us/ManageYourProducts/GlobalSettings/AccessControl/APICredentials/).
2. Select Add Credential, and enter a name and a description.
3. Choose the role Service Principal Read-Only.
4. Select Add. Sophos creates a client ID and a client secret.
5. Copy the client ID and the client secret. You can see the client secret only once.

## Fields

| Field | What to enter |
|-------|---------------|
| Client ID | The client ID of the API credential. |
| Client Secret | The client secret of the same credential. Sophos shows it once, when you create the credential, so copy it then. |

You do not enter an address. Sophos tells Arch which regional host holds your account's data.

## Permissions

| Permission | What Arch reads with it |
|------------|-------------------------|
| Service Principal Read-Only | The account's computer list and each computer's details. Arch only reads with it. |

You choose the role when you add the credential. If a credential has another role, add a new credential with
Service Principal Read-Only and enter its client ID and secret in Arch. See [API Credentials](https://docs.sophos.com/central/customer/help/en-us/ManageYourProducts/GlobalSettings/AccessControl/APICredentials/).

## Sign-in

Arch signs in by exchanging the client ID and the client secret for a Sophos token. When the sign-in works, the
connection test goes on to ask Sophos which account the credential belongs to, where its data is held, and how
many computers it lists.

If the sign-in fails, check that you copied the client ID and the client secret of the same credential. If the
credential was deleted or has expired, add a new one under Global Settings, then Access Control, then API
Credentials, in Sophos Central. Sophos removes an expired credential without an alert.

## Test answers

A passing test shows "Computers in Sophos" with the number of computers Sophos lists for the account.

| Message | What it means and what to do |
|---------|------------------------------|
| These Sophos credentials are incomplete. | A field is empty. Enter both the client ID and the client secret. |
| Sophos refused this client ID and secret. | Sophos did not accept the credential. Check both values. If the credential was deleted or its secret has expired, create a new one. |
| This Sophos credential cannot list computers. | The credential does not have the role Service Principal Read-Only. Create a credential with that role, then enter its client ID and secret. |
| This credential belongs to a Sophos partner account. | The credential was created in a partner, organization or distributor account. Create it inside the Sophos Central account that manages the computers. |
| This credential does not belong to one Sophos Central account. | Sophos did not name one account for the credential. Create the credential inside the Sophos Central account that manages the computers. |
| Sophos did not say where this account's data is. | Sophos gave no data region. Try again in a few minutes. If it keeps happening, contact Arch support. |
| Sophos named a data region Arch will not send this credential to. | Arch sends the credential only to Sophos's own regional hosts. Try again in a few minutes. If it keeps happening, contact Arch support. |
| Sophos is temporarily unavailable. | Sophos is down or is rate-limiting the credential. Try again in a few minutes. |
| Sophos did not answer conclusively. | Arch could not reach Sophos or could not read its answer. Try again in a few minutes. |

For an organization or distributor credential, the message names that account type instead of partner.

## Limits

- Arch brings in every computer Sophos Central lists for the account: its name, operating system and network
  addresses, and its serial number and disk encryption state where Sophos reports them.
- Servers, detections, alerts and the person who uses a computer are not brought in.
- Arch reads the data once a day by default. You can choose every hour, every 3, 6 or 12 hours, or once a day.
- Each run reads the whole computer list, because Sophos cannot list only the computers that changed.
- One Sophos Central account connects to Arch once. A second connection to the same account is refused.

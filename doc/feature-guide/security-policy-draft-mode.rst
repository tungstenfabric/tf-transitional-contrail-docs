.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

=====================================
Security Policies Draft Mode Overview
=====================================

Starting with Contrail release 5.0, you can create new security policies and edit existing security polices in a draft mode. The draft mode ensures that a system administrator can review and validate all policies before enforcing them. The draft mode functionality is disabled, by default. When the draft mode functionality is enabled, security policies are listed in the following three views:

-  **Committed** —View the policies that are already enforced


-  **Drafted** —View, create, and edit policies in the draft mode


-  **Review** —Review the drafted policies and commit or discard the drafts


The draft mode functionality is available in both global and project scopes and enables you to perform the following functions:

- Create new policies—All new policies are created in the draft mode and are not immediately enforced. Before the new policies are enforced, any modifications to these policies are applied only on the draft versions. You can enforce the policy by committing the policy in the **Review** view. If you choose to not enforce the draft policy, you can also discard all modifications which deletes the new draft policy.


- Modify existing policies—When you modify an existing enforced policy, a clone of the policy is created in the draft mode. Draft clones have the same name as the original policy but have a different and unique UUID. All modifications are applied to the cloned policy and not enforced on the original policy. When the modified clone policy is committed, it over-writes the original policy and the clone is removed from the draft mode. If you choose to not enforce the edited policy, you can also discard all modifications to the cloned policy.


- Delete existing policies—When an enforced policy is deleted, a clone of the policy is created in the draft mode and the clone is flagged for deletion. A policy flagged for deletion cannot be edited. If you choose to not delete the policy, you can also discard the delete action on the cloned policy.


After reviewing the policies in the draft mode, a system administrator can choose to commit or discard all modifications. The commit and discard actions apply to all the policies listed in the **Review** view and are dependent on a  draft_mode_stateenumerated string. All policies are tagged with a  draft_mode_stateenumerated string which is assigned different values depending on the state of the policies. The enumerated string values for newly created drafts are set to  draft_mode_state==created, modified draft clones are set to  draft_mode_state==updated, and policy clones flagged for deletion are set to  draft_mode_state==deleted. The enumerated string for enforced policies is set to  None.

A system administrator can choose to perform one of the following actions in the **Review** view:

- Commit—When a policy is reviewed and validated, the security administrator can commit the policy to enforce it. A committed policy is enforced only in the scope in which it was created. The commit action ensures the following:

- Newly created policies or policies whose  draft_mode_state==createdare enforced and are visible in the **Committed** view. The  draft_mode_stateof the enforced policy is set to  None.


- Edited policies or policies whose  draft_mode_state==updatedare enforced and are visible in the **Committed** view. The  draft_mode_stateof the original policy remains unchanged at  None. The draft clones are removed from the **Drafted** view.


- Policies flagged for deletion or policies whose  draft_mode_state==deletedare deleted. The enforced policies as well as the draft clones are removed.



- Discard—When a policy is not validated, the security administrator can abandon or discard all changes to the policy. The discard action ensures the following:

- Newly created policies are deleted and are removed from the **Drafted** view.


- Edits to enforced policies are ignored and the draft clones are removed. The original policy remains unchanged.


- Policies flagged for deletion are ignored. The  draft_mode_state==deletedflag is removed and the draft clone is deleted. The original policy remains unchanged.




.. note:: You cannot make any modifications to a policy when the policy is being committed or discarded.



The draft mode functionality is enabled for the following security policy resources:

- Application Policy Set


- Firewall Policy


- Firewall Rule


- Service Group


- Address Group


**Related Documentation**

-  `Managing Security Policies Draft Mode`_ 


.. _Managing Security Policies Draft Mode: security-policy-draft-mode-managing.html

.. _Security Policy Enhancements: 


## Implementation Outline

Here are the steps that needs to be followed to implement the feature:

1. Create 3 new tables in the database. Generate migration files and make the necessary changes to the model files and repository files.
   - focus_time_scheduled

     ```
     CREATE TABLE focustime_schedules (
       id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
       user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
       name TEXT, -- optional (e.g., "Default Work Hours")
       timezone TEXT NOT NULL, -- important!
       created_at TIMESTAMP DEFAULT now(),
       updated_at TIMESTAMP DEFAULT now()
     );
     ```

   - weekly_time_slots

     ```
     CREATE TABLE weekly_time_slots (
       id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
       schedule_id UUID NOT NULL REFERENCES focustime_schedules(id) ON DELETE CASCADE,

       day_of_week SMALLINT NOT NULL CHECK (day_of_week BETWEEN 0 AND 6),
       -- 0 = Sunday, 1 = Monday ... 6 = Saturday

       start_time TIME NOT NULL,
       end_time TIME NOT NULL,

       CHECK (start_time < end_time)
     );
     ```

   - schedule_email_threads

   ```
   CREATE TABLE schedule_email_threads (
     schedule_id UUID NOT NULL REFERENCES focustime_schedules(id) ON DELETE CASCADE,
     thread_id UUID NOT NULL REFERENCES email_threads(id) ON DELETE CASCADE,

     PRIMARY KEY (schedule_id, thread_id)
   );
   ```

2. Create APIs to create and update the focus time and update the email threads included in that focus time.
   - Handle the timezone conversion for the focus time and weekly time slots.
   - Handle the validation of the focus time and weekly time slots.
   - Utilize the existing time slots if already present in the database for that user.

3. Create a modal to display the focus time and weekly time slots.
   - UI should have the option to select the day of the week and time window for that day of the week.

4. Create a new UI component/screen to display the focus time and weekly time slots.
   - Display the the list of focus time slots with email threads attached in that focus time.
   - Allow the user to add or remove email threads from the focus time.

5. Add option to snooze a particular email thread on hovering over the email thread. And give the same option of email thread's view page.

6. When user selects the email threads, add an option to snooze email threads on options menu.
   - If the user selects multiple email threads, and few of them are already snoozed, then they will be updated with the new scheduled focus time selected by the user. If not already snoozed, they will be snoozed with the new scheduled focus time selected by the user.

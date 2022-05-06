---
id: integration-with-directual
title: Integration with Directual
sidebar_label: Integration with Directual
---


Let's create a task manager using [Directual](https://www.directual.com/).

# 1 Setting up Directual

## 1.1 Creating a Directual Project

Create a blank app. To do this, click **Create a blank app**.

If you already have apps, you need to click **New app**.

![Create New Application](/scr/tutorials/integration-with-directual-create-new-application.png)

In the window that appears, enter **System name**, the rest of the fields are optional.

![New Application Form](/scr/tutorials/integration-with-directual-new-application-form.png)


After that, our application will appear in the **My Applications** list, click on it.

![My Applications](/scr/tutorials/integration-with-directual-my-applications.png)


We got into **Dashboard**.

## 1.2 Creating structures

For our application to work, we need to create two **[Data structures](https://readme.directual.com/data/data-structures)**:

- Tasks. This is where user tasks will be stored.
- Register requests. This is where user registration requests will be stored.

To create a database, go to **Database**.

![App Dashboard](/scr/tutorials/integration-with-directual-app-dashboard.png)

To do this, click **+ Create new...** and select **Data structure** from the drop-down list.

![App Database](/scr/tutorials/integration-with-directual-app-database.png)

Create a Tasks structure with these parameters:

- Structure name: `Tasks`
- System name: `tasks`

![Create New Data Structure Tasks](/scr/tutorials/integration-with-directual-create-new-data-structure-tasks.png)


Click **Save and go**. This will take us to the page with our created structure.

Next, we need to configure the structure fields. To do this press the **Configure fields** button.

Let's create these fields:

| System name | Display name | Data type |
| --- | --- | --- |
| id | id | id |
| description | Description | string |
| completed | Completed | boolean |
| user | user | link App users [WebUser] |

Add an Internal group, and in it:

| System name | Display name | type |
| --- | --- | --- |
| isDeleted | Is deleted | boolean |

![Configure Fields](/scr/tutorials/integration-with-directual-configure-fields-tasks.png)

Press **Save and exit**.

Then press **Database** to return to the list of structures.

Next, create a Register requests structure with these parameters:

- Structure name: `Register requests`
- System name: `register_requests`

![Create New Data Structure Register Requests](/scr/tutorials/integration-with-directual-create-new-data-structure-register-requests.png)

Click **Save and go**. This will take us to the page with our created structure.

Next we need to configure the fields of the structure. To do this press the **Configure fields** button.

Let's create these fields:

The **Main group**

| System name | Display name | Data type |
| --- | --- | --- |
| id | Username (login) | id |
| password | Password | password [string] |
| completed | Completed | boolean |

The **Response** group

| System name | Display name | Data type |
| --- | --- | --- |
| success | Success | string |
| error | Error | string |

![Configure fields Register Requests](/scr/tutorials/integration-with-directual-configure-fields-register-requests.png)


Press **Save and exit**.

# 1.3 Creating scenarios

For our application to work, we need to create two scenarios (https://readme.directual.com/scenarios/principles-of-scenarios):

- Delete task. This is where the task will be deleted.
- Create user. This is where user registration will take place.

To create scenarios, go to **Scenarios** and click **+ New scenario**.

For the first scenario we specify the following parameters:

- Scenario name: `Delete task`
- Target data structure: `Tasks [tasks]`
- Run scenario by: `Real-time: Changed objects`
- Trigger by fields `Is deleted`

![Create New Scenario](/scr/tutorials/integration-with-directual-create-new-scenario.png)


Then click **Save**.

Our new scenario now appears in the list. Click on it to edit it.

![All Scenarios](/scr/tutorials/integration-with-directual-all-scenarios.png)

The **Delete task** scenario will work like this: 

- If **Is deleted** field is **true**, we delete our object.
- Else we don't do anything.

This is how it is implemented in Directual:

![Delete Task](/scr/tutorials/integration-with-directual-delete-task.png)


In the **Condition** block set 

- Is deleted
- equal
- true.

Then click **Save**.

![Condition Settings](/scr/tutorials/integration-with-directual-condition-settings.png)

Press **Publish draft**.

![Publish Delete Task](/scr/tutorials/integration-with-directual-publish-delete-task.png)

And then **Run scenario**.

![Run Delete Task](/scr/tutorials/integration-with-directual-run-delete-task.png)

After performing these steps, our scenario will be launched (indicated by the green triangle next to the name).

![Play Delete Task](/scr/tutorials/integration-with-directual-play-delete-task.png)

Back to the list of scenarios.

Press **+ New scenario** to create a second scenario**.

Specify these parameters:

- Scenario name: `Create user`
- Target data structure: `Register requests [register_requests]`
- Run scenario by: `Manually or By schedule`

![Create New Scenario Create User](/scr/tutorials/integration-with-directual-create-new-scenario-create-user.png)

In the **Context variables** tab add this parameter:

| SysName | Field name | Type | default value |
| --- | --- | --- | --- |
| users_count | Users count | number | 0 |

Then click **Save**.

![Scenario Starting Parameters](/scr/tutorials/integration-with-directual-scenario-starting-parameters.png)

Our new scenario now appears in the list. Click on it to edit it.

![All Scenarios](/scr/tutorials/integration-with-directual-all-scenarios-with-create-user.png)

The **Create user** script will work like this:

1. Count the number of users with the login from the request (register request);
2. If the number of users is 0 (there is no user with such login), then create and return the answer;
3. Else an error is returned.

This is how it is implemented in Directual:

![Create New User Scenario](/scr/tutorials/integration-with-directual-create-new-user-scenario.png)

In the Search block we specify the following parameters:

- Search objects in structure: `App users [WebUser]`
- Find objects and `count them`
- Save the result to `Users count from ContextVars`

![Find Objects Parameters](/scr/tutorials/integration-with-directual-find-objects-parameters.png)


In the Search conditions tab we specify: 

- `Username (login) from WebUser`
- `equal`
- `#{{id}}`

Then click Save.

![Find Objects Conditions](/scr/tutorials/integration-with-directual-find-objects-conditions.png)


In the **Condition** block we specify:

- `Users count from ContextVars`
- `equal`
- `0`

Then click **Save**.

![Find Objects Condition](/scr/tutorials/integration-with-directual-find-objects-condition.png)

In the **Create object** block we specify:

- Create an object in structure `App users [WebUser]`
- ID of new object `Set ID manually`
- Set the ID of the object `#{{id}}`

![Create Object](/scr/tutorials/integration-with-directual-app-users-create-object-parameters.png)

In the **Fields mapping** tab we specify:

- Password (hash): `{{password}`

Then click **Save**.

![Create Object Fields Mapping](/scr/tutorials/integration-with-directual-app-users-create-object-fields-mapping.png)


In the **Edit object** block that follows Create object in the Yes branch, specify:

- Success from register_requests: `Successfully registered!`
- Error from register_requests: *`Leave empty`*

Then click **Save**.

![Edit Object Success Registration](/scr/tutorials/integration-with-directual-app-users-edit-object-success-registration.png)

In the **Edit object** block, which is in the No branch, specify:

- Error from register_requests: `User exists!`
- Success from register_requests: *`Leave empty`*

Then click **Save**.

![Edit Object Error Registration](/scr/tutorials/integration-with-directual-app-users-edit-object-error-registration.png)




Press **Publish draft** and **Run scenario**.

![Play Create User](/scr/tutorials/integration-with-directual-play-create-user.png)

There will now be two running scripts in the list.

![All Scenarios](/scr/tutorials/integration-with-directual-all-scenarios-with-played-create-user.png)


# 1.4 Creating API-Endpoints

For Directual to work with Quarkly, you need to create several [API-Endpoints](https://readme.directual.com/api-integrations/api-endpoints-security-layer):

- tasks/tasks - for creating, editing and deleting tasks
- register_requests/create_user - to register a user

To create API-Endpoints, go to the API section.

![App API](/scr/tutorials/integration-with-directual-app-api.png)


Press **+ New API-endpoint**.

For the endpoint tasks/tasks we use the following parameters:

- Conditions on user’s session (structure App users): `id isNotNull;`
- GET: `completed, description, id`
- POST: `completed, description, id, user, isDeleted`
- Filter object from tasks: `user.id == {{id}}`
- Enable cors: `true`

Then click **Save and exit**.

![API Endpoint Configuration Tasks](/scr/tutorials/integration-with-directual-api-endpoint-configuration-tasks-part-1.png)

![API Endpoint Configuration Tasks](/scr/tutorials/integration-with-directual-api-endpoint-configuration-tasks-part-2.png)

![API Endpoint Configuration Tasks](/scr/tutorials/integration-with-directual-api-endpoint-configuration-tasks-part-3.png)

![API Endpoint Configuration Tasks](/scr/tutorials/integration-with-directual-api-endpoint-configuration-tasks-filter-part-4.png)

For the endpoint register_requests/create_user we use these parameters:

- Conditions on user’s session (structure App users): `no conditions`
- GET: `error, success`
- POST: `id, password`
- Filter object from tasks: `no conditions`
- Enable cors: `true`

Then click **Save and exit**.

![API Endpoint Configuration Registration Requests](/scr/tutorials/integration-with-directual-api-endpoint-configuration-reg-requests-part-1.png)

![API Endpoint Configuration Registration Requests](/scr/tutorials/integration-with-directual-api-endpoint-configuration-reg-requests-part-2.png)

![API Endpoint Configuration Registration Requests](/scr/tutorials/integration-with-directual-api-endpoint-configuration-reg-requests-part-3.png)


# 1.5 Configuring security settings for the API

In the API section, go to the **Security settings** tab.

Turn on CORS for authorization functions, and add domains to the list:

- `https://quarkly.io/`
- *`Your domain on which the published application will run.`*

Then click **Save settings**.

![API Security Settings](/scr/tutorials/integration-with-directual-api-security-settings.png)


# 2 Setting up a Quarkly project

Create an empty project in Quarkly.

## 2.1 DirectualClient component (module)

Create a DirectualClient component. This will be the module with our Directual project's parameters. It will export the useTasks hook to work with the task list and useAuth hook to work with authorization.

The [swr](http://swr.vercel.app) library is used to sample the data.

Copy the code below and paste it into our component.

```jsx
import Directual from 'directual-api';
import { useCallback, useMemo, useState, useEffect } from 'react';
import useSWRInfinite from 'swr/infinite';
import md5 from 'md5-hash';

const appID = '<YOUR_APP_ID>';
const apiHost = 'https://api.directual.com';

const api = new Directual({
    appID,
    apiHost,
});

/*
 * Fetch for swr
 * Read more: https://swr.vercel.app/docs/data-fetching
 */
const tasksFetcher = ({ pageIndex }, sessionID) =>
    api.structure('tasks').getData('tasks', {
        sessionID,
        page: pageIndex,
    });

/*
 * Hook to work with the task list
 */
export const useTasks = (user) => {
    const { sessionID, username } = user || {};

    /*
     * Getting task data
     * Read more: https://swr.vercel.app/docs/pagination#useswrinfinite
     */
    const { data, error, size, setSize, mutate } = useSWRInfinite(
        (pageIndex) => {
            if (!sessionID) return null;

            return [{ pageIndex }, user.sessionID];
        },
        tasksFetcher
    );

    const maxPage = data?.[data.length - 1]?.pageInfo?.totalPage;
    const isLoadingMore = maxPage > size;

    const fetchMore = useCallback(() => {
        if (!isLoadingMore) return null;

        setSize((x) => {
            return x + 1;
        });
    }, [isLoadingMore, setSize]);

    // Changing task data
    const mutateTaskById = useCallback(
        async (id, newObjData) => {
            mutate(
                (x) =>
                    x.map((r) => ({
                        ...r,
                        payload: r.payload.map((task) => {
                            if (task.id === id)
                                return { ...task, ...newObjData };
                            return task;
                        }),
                    })),
                false
            );

            await api
                .structure('tasks')
                .setData('tasks', { id, ...newObjData }, { sessionID });

            mutate();
        },
        [mutate, sessionID]
    );

    const deleteTaskById = useCallback(
        async (id) => {
            mutate(
                (x) =>
                    x.map((r) => ({
                        ...r,
                        payload: r.payload.filter((task) => task.id !== id),
                    })),
                false
            );

            await api
                .structure('tasks')
                .setData('tasks', { id, isDeleted: true }, { sessionID });

            setTimeout(mutate, 1000);
        },
        [mutate, sessionID]
    );

    const addTask = useCallback(
        async (task) => {
            await api
                .structure('tasks')
                .setData('tasks', { ...task, user: username }, { sessionID });

            mutate();
        },
        [mutate, sessionID, username]
    );

    const flat = useMemo(
        () =>
            data
                ?.map((x) => x.payload)
                ?.flat(1)
                ?.map((task) => {
                    return {
                        ...task,
                        mutate: (obj) => mutateTaskById(task.id, obj),
                        delete: () => deleteTaskById(task.id),
                    };
                }),
        [data, deleteTaskById, mutateTaskById]
    );

    return {
        data: flat,
        error,
        fetchMore,
        isLoadingMore,
        addTask,
    };
};

/*
 * Hook to work with authorization
 */
export const useAuth = () => {
    const [user, setUser] = useState(null);

    const signin = useCallback((username, password) => {
        return api.auth
            .login(username, password)
            .then((res) => {
                setUser(res);
                window.localStorage.setItem('sid', res.sessionID);
            })
            .catch((e) => {
                throw new Error(e?.response?.data?.msg ?? e.response);
            });
    }, []);

    const signout = useCallback(() => {
        api.auth.logout(user.sessionID);
        setUser(null);
        window.localStorage.setItem('sid', null);
    }, [user.sessionID]);

    const signup = useCallback(async (username, password) => {
        const res = await api
            .structure('register_requests')
            .setData('create_user', { id: username, password: md5(password) });

        if (res.result[0].error) throw new Error(res.result[0].error);

        return res.result[0];
    }, []);

    useEffect(() => {
        async function init() {
            const sid = window.localStorage.getItem('sid');
            if (!sid) return;

            const res = await api.auth.check(sid);
            if (!res) return;

            setUser(res);
        }

        if (!window) return;
        init();
    }, []);

    return {
        user,
        signin,
        signout,
        signup,
    };
};

export default api;
```

You must also replace `<YOUR_APP_ID>` with your application id. This can be obtained in the Endpoint respond preview in any of the endpoints.

![Endpoint Respond Preview](/scr/tutorials/integration-with-directual-endpoint-respond-preview.png)


## 2.2 App component

Create an App component. The App component is the wrapper for our entire application. Here, we will call hooks from the Directual client and pass their results through [React Context](https://reactjs.org/docs/context.html).

Copy the code below and paste it into our component.

```jsx
import React, { createContext, useContext } from 'react';
import { Box } from '@quarkly/widgets';
import {
    useTasks as useTasksOriginal,
    useAuth as useAuthOriginal,
} from './DirectualClient';

const TasksContext = createContext({});
const AuthContext = createContext({});

export const useTasks = () => useContext(TasksContext);
export const useAuth = () => useContext(AuthContext);

const App = ({ children, ...props }) => {
    const authValue = useAuthOriginal();
    const tasksValue = useTasksOriginal(authValue.user);

    return (
        <Box {...props}>
            <AuthContext.Provider value={authValue}>
                <TasksContext.Provider value={tasksValue}>
                    {children}
                </TasksContext.Provider>
            </AuthContext.Provider>
        </Box>
    );
};

export default Object.assign(App, {
    title: 'App',
    description: {
        en: 'App — my awesome component',
    },
    propInfo: {},
});
```

## 2.3 Input, Checkbox, and Form components from the Marketplace

You will need several components from the catalog to make our application work:

- Input
- Checkbox
- Form

Find them in the components catalog and add them to the project.

## 2.4 LoginForm component

Create a LoginForm component. It will be the login form.

Copy the code below and paste it into our component.

```jsx
import React, { useState, useCallback } from 'react';
import { Button, Box, useConstructorMode } from '@quarkly/widgets';
import { useOverrides } from '@quarkly/components';
import { useAuth } from './App';
import Form from './QuarklycommunityKitForm';

// Object with overrides
// Read more about overrides: https://developers.quarkly.io/components/overrides/overview
const overrides = {
    'Sign In Form': {
        kind: 'Form',
        props: {},
    },
    'Sign Up Form': {
        kind: 'Form',
        props: {},
    },
    'Sign Out Button': {
        kind: 'Button',
        props: {
            children: 'Sign Out',
        },
    },
    'Switch Button': {
        kind: 'Button',
    },
    'Switch Button to Sign In': {
        kind: 'Button',
        props: {
            children: 'I have an account',
        },
    },
    'Switch Button to Sign Up': {
        kind: 'Button',
        props: {
            children: 'Create account',
        },
    },
};

const getAPI = () => {
    if (typeof window !== 'undefined') {
        return window.QAPI || {};
    }
    if (typeof global !== 'undefined') {
        return global.QAPI || {};
    }
    return {};
};

const LoginForm = (props) => {
    const { override, rest, ChildPlaceholder } = useOverrides(props, overrides);
    const { user, signin, signout, signup } = useAuth();
    const [isLogin, setIsLogin] = useState(true);
    const [error, setError] = useState('');
    const [success, setSuccess] = useState('');

    const mode = useConstructorMode();

    const onSubmit = useCallback(
        async (e) => {
            e.preventDefault();

            const isDev = getAPI().mode === 'development';
            if (isDev && mode === 'constructor') return;

            const data = new FormData(e.target);

            setError('');

            try {
                const username = data.get('username');
                const password = data.get('password');

                if (isLogin) {
                    await signin(username, password);
                } else {
                    const { success: successMessage } = await signup(
                        username,
                        password
                    );
                    setSuccess(successMessage);
                    setIsLogin(true);
                }
            } catch (err) {
                setSuccess('');
                setError(err.message);
            }
        },
        [isLogin, mode, signin, signup]
    );

    const switchForm = useCallback(() => {
        const isDev = getAPI().mode === 'development';
        if (isDev && mode === 'constructor') return;

        setIsLogin((x) => !x);
        setError('');
    }, [mode]);

    const onSignOut = useCallback(() => {
        signout();
    }, [signout]);

    const switchButtonOverride = `Switch Button to Sign ${
        isLogin ? 'Up' : 'In'
    }`;

    return (
        <Box {...rest}>
            {user ? (
                <Button onClick={onSignOut} {...override('Sign Out Button')} />
            ) : (
                <>
                    {isLogin ? (
                        <Form
                            onSubmitCb={onSubmit}
                            {...override(`Sign In Form`)}
                        >
                            <ChildPlaceholder slot={'Sign In Form'} />
                            <></>
                        </Form>
                    ) : (
                        <Form
                            onSubmitCb={onSubmit}
                            {...override(`Sign Up Form`)}
                        >
                            <ChildPlaceholder slot={'Sign Up Form'} />
                            <></>
                        </Form>
                    )}
                    <Box {...override('Error message')}>{error}</Box>
                    <Box {...override('Succes message')}>{success}</Box>
                    <Button
                        onClick={switchForm}
                        {...override('Switch Button', switchButtonOverride, {
                            defaultKey: switchButtonOverride,
                        })}
                    />
                </>
            )}
        </Box>
    );
};

export default Object.assign(LoginForm, {
    title: 'LoginForm',
    description: {
        en: 'LoginForm — my awesome component',
    },
    propInfo: {},
});
```

## 2.5 The ButtonWithIcon component

Create a ButtonWithIcon component. It will be a button with an icon.

Copy the code below and paste it into our component.

```jsx
import React from 'react';
import { Button, Icon } from '@quarkly/widgets';
import { useOverrides } from '@quarkly/components';

// Object with overrides
// Read more about overrides: https://developers.quarkly.io/components/overrides/overview
const overrides = {
    Icon: {
        kind: 'Icon',
        props: {
            category: 'fa',
            icon: 'FaPlus',
        },
    },
};

const ButtonWithIcon = (props) => {
    const { override, rest } = useOverrides(props, overrides);

    return (
        <Button {...rest}>
            <Icon {...override('Icon')} />
        </Button>
    );
};

export default Object.assign(ButtonWithIcon, {
    title: 'ButtonWithIcon',
    description: {
        en: 'ButtonWithIcon — my awesome component',
    },
    overrides,
    propInfo: {},
});
```

## 2.6 Task component

Create Task component. This will be a component for displaying a single task.

Copy the code below and paste it into our component.

```jsx
import React, { useState, useEffect, useCallback } from 'react';
import { Box, Input } from '@quarkly/widgets';
import { Override, useOverrides } from '@quarkly/components';
import Checkbox from './QuarklycommunityKitCheckbox';
import ButtonWithIcon from './ButtonWithIcon';

// Object with overrides
// Read more about overrides: https://developers.quarkly.io/components/overrides/overview
const overrides = {
    Text: {
        kind: 'Input',
    },
    'Completed checkbox': {
        kind: 'Checkbox',
    },
    'Delete button': {
        kind: 'ButtonWithIcon',
        props: {},
    },
};

const Task = ({ task, ...props }) => {
    const { override, rest } = useOverrides(props, overrides);
    const [description, setDescription] = useState(task.description);

    const onCompletedChange = useCallback(
        (e) => {
            task.mutate({
                completed: e.target.checked,
            });
        },
        [task]
    );

    const onInputChange = useCallback((e) => {
        setDescription(e.target.value);
    }, []);

    const onInputBlur = useCallback(() => {
        if (description !== task.description) task.mutate({ description });
    }, [description, task]);

    const onDeleteClick = useCallback(() => {
        task.delete();
    }, [task]);

    useEffect(() => {
        setDescription(task.description);
    }, [task.description]);

    return (
        <Box display="flex" {...rest}>
            <Checkbox
                checked={task?.completed}
                onChange={onCompletedChange}
                {...override('Checkbox')}
            />
            <Input
                value={description}
                onChange={onInputChange}
                onBlur={onInputBlur}
                {...override(
                    'Description',
                    task.completed && 'Description Completed'
                )}
            />
            <ButtonWithIcon
                {...override('Delete button')}
                onClick={onDeleteClick}
            >
                <Override slot="Icon" category="fa" icon="FaTrashAlt" />
                {override('Delete button').children}
            </ButtonWithIcon>
        </Box>
    );
};

export default Object.assign(Task, {
    title: 'Task',
    description: {
        // paste here description for your component
        en: 'Task — my awesome component',
    },
    overrides,
    propInfo: {},
});
```

## 2.7 Tasks component

Create a component called Tasks. This will be a list of tasks.

Copy the code below and paste it into our component.

```jsx
import React from 'react';
import { Box, Button, Text } from '@quarkly/widgets';
import { useOverrides } from '@quarkly/components';
import Task from './Task';
import { useTasks, useAuth } from './App';

// Object with overrides
// Read more about overrides: https://developers.quarkly.io/components/overrides/overview
const overrides = {
    Task: {
        kind: 'Task',
    },
    'Sign In Message': {
        kind: 'Text',
        props: {
            children: 'Please sign in to add and view tasks!',
        },
    },
};

const Tasks = (props) => {
    const { override, rest } = useOverrides(props, overrides);
    const { data, isLoadingMore, fetchMore } = useTasks();
    const { user } = useAuth();

    return (
        <Box {...rest}>
            {user ? (
                <>
                    {data?.map((task) => (
                        <Task
                            key={task.id}
                            task={task}
                            {...override('Task', `Task ${task.id}`)}
                        />
                    ))}
                    {isLoadingMore && (
                        <Button onClick={fetchMore}>Load more</Button>
                    )}
                </>
            ) : (
                <Text {...override('Sign In Message')} />
            )}
        </Box>
    );
};

export default Object.assign(Tasks, {
    title: 'Tasks',
    description: {
        // paste here description for your component
        en: 'Tasks — my awesome component',
    },
    overrides,
    propInfo: {},
});
```

## 2.8 AddTask component

Create a component called AddTask. This will be a component for adding new tasks.

Copy the code below and paste it into our component.

```jsx
import React, { useState, useCallback } from 'react';
import { Box } from '@quarkly/widgets';
import { useOverrides } from '@quarkly/components';
import Input from './QuarklycommunityKitInput';
import ButtonWithIcon from './ButtonWithIcon';
import { useTasks, useAuth } from './App';

const overrides = {
    Input: {
        kind: 'Input',
        props: {},
    },
    'Add button': {
        kind: 'ButtonWithIcon',
        props: {},
    },
};

const AddTask = (props) => {
    const { override, rest } = useOverrides(props, overrides);
    const [description, setDescription] = useState('');
    const { user } = useAuth();
    const { addTask } = useTasks();

    const onSubmit = useCallback(() => {
        addTask({
            description,
            completed: false,
        });
    }, [addTask, description]);

    const onChange = useCallback((e) => {
        setDescription(e.target.value);
    }, []);

    return (
        <Box display="inline-flex" {...rest}>
            {user && (
                <>
                    <Input
                        {...override('Input')}
                        value={description}
                        onChange={onChange}
                    />
                    <ButtonWithIcon
                        {...override('Add button')}
                        onClick={onSubmit}
                    />
                </>
            )}
        </Box>
    );
};

export default Object.assign(AddTask, {
    title: 'AddTask',
    description: {
        en: 'AddTask — my awesome component',
    },
    overrides,
    propInfo: {},
});
```

## 2.9 Setting up the home page

Copy the code below and paste it into our page.

```jsx
<Components.App>
	<Text margin="0px 0px 0px 0px" font="--headline1" text-align="center">
		Tasks
	</Text>
	<Box
		min-width="100px"
		min-height="100px"
		margin="0px auto 0px auto"
		max-width="500px"
		padding="0px 20px 0px 20px"
	>
		<Components.Tasks>
			<Override slot="Task" padding="10px 0px 10px 0px">
				<Override slot="Checkbox">
					<Override slot="Text" display="none" />
				</Override>
				<Override
					slot="Description"
					align-self="center"
					width="100%"
					border-width="2px"
					focus-border-width="2px"
					border-color="rgba(255, 255, 255, 0)"
					focus-border-color="--color-primary"
				/>
				<Override slot="Description Completed" text-decoration-line="line-through" />
				<Override
					slot="Delete button"
					padding="0px 0px 0px 0px"
					width="20px"
					height="20px"
					background="rgba(247, 251, 255, 0)"
					align-self="center"
					color="--darkL2"
				>
					<Override slot="Icon" size="12px" margin="0px auto 0px auto" color="--darkL2" />
				</Override>
			</Override>
			<Override slot="Icon" category="fa" icon="FaArtstation" />
		</Components.Tasks>
		<Components.LoginForm>
			<Override slot="Sign In Form">
				<Text font="--headline3" text-align="center">
					Sign In
				</Text>
				<Input
					display="block"
					placeholder-color="LightGray"
					background="white"
					name="username"
					placeholder="Username"
					required
					sm-width="100%"
					margin="0px auto 10px auto"
				/>
				<Input
					display="block"
					placeholder-color="LightGray"
					background="white"
					name="password"
					type="password"
					placeholder="Password"
					required
					sm-width="100%"
					margin="0px auto 10px auto"
				/>
				<Button margin="0px auto 0px auto" display="block">
					Submit
				</Button>
			</Override>
			<Override slot="Sign Up Form">
				<Text text-align="center" font="--headline3">
					Sign Up
				</Text>
				<Input
					display="block"
					placeholder-color="LightGray"
					background="white"
					name="username"
					placeholder="Username"
					required
					sm-width="100%"
					margin="0px auto 10px auto"
				/>
				<Input
					display="block"
					placeholder-color="LightGray"
					background="white"
					name="password"
					type="password"
					placeholder="Password"
					required
					sm-width="100%"
					margin="0px auto 10px auto"
				/>
				<Button margin="0px auto 0px auto" display="block">
					Submit
				</Button>
			</Override>
			<Override
				slot="Switch Button"
				background="rgba(255, 255, 255, 0)"
				color="--dark"
				text-decoration-line="underline"
				font="--base"
				focus-box-shadow="none"
			/>
			<Override slot="Error message" text-align="center" margin="10px 0px 0px 0px" color="--red" />
			<Override slot="Succes message" text-align="center" color="--green" />
			<Text margin="0px 0px 0px 0px" font="--headline3">
				Sign In
			</Text>
		</Components.LoginForm>
	</Box>
</Components.App>
```

After that the index page will look like this:

![Screenshot Index Page](/scr/tutorials/integration-with-directual-result-index-page.png)


---

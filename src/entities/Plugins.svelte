<script>
    import {Route, meta} from 'tinro';
	import List from '../components/List.svelte';
    import Details from '../components/Details.svelte';
    import Create from '../components/Create.svelte';
    import Date from '../components/Date.svelte';
</script>

<Route path="/">
    <List entity="plugins" let:data let:entity>
        <table class="table card-table table-vcenter text-nowrap datatable">
            <thead>
                <tr>
                    <th class="w-1">
                        <input class="form-check-input m-0 align-middle" type="checkbox" aria-label="Select all invoices">
                    </th>
                    <th>Name</th>
                    <th>Route</th>
                    <th>Service</th>
                    <th>Protocols</th>
                    <th>Methods</th>
                    <th class="text-end">Created at</th>
                </tr>
            </thead>
            <tbody>
                {#each data as record, i}
                    <tr>
                        <td>
                            <input class="form-check-input m-0 align-middle" type="checkbox">
                        </td>
                        <td>
                            <a href="/{entity}/{record.id}" class="text-reset">
                                {record.name}
                            </a>
                        </td>
                        <td>{record.route}</td>
                        <td>
                            <a href="/services/{record.service.id}" class="text-reset">
                                {record.service.id}
                            </a>
                        </td>
                        <td>
                            {#each record.protocols as protocol}
                                <span class="badge bg-blue-lt me-1">
                                    {protocol}
                                </span>
                            {/each}
                        </td>
                        <td>
                            {#if record.methods}
                                {#each record.methods as method}
                                    <span class="badge bg-green-lt me-1">
                                        {method}
                                    </span>
                                {/each}
                            {/if}
                        </td>
                        <td class="text-end">
                            <Date timestamp="{record.created_at}" />
                        </td>
                    </tr>
                {/each}
            </tbody>
        </table>
    </List>
</Route>


<Route path="/add">
    <Create entity="plugins" />
</Route>


<Route path="/:id" let:meta>
    <Details entity="plugins" id="{meta.params.id}" let:data />
</Route>
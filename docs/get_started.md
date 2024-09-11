# Get started

This section will guide you to your first occurrence cube. It refers, to and is based on the [GBIF API SQL Downloads](https://techdocs.gbif.org/en/data-use/api-sql-downloads) and the [Species occurrence cubes](https://techdocs.gbif.org/en/data-use/data-cubes) documentation.

## Requirements

Check the following:
- You have a working GBIF account
- You have access to a shell (Windows users: a prompt DOS, that black old school window)
- You can run curl commands. Check you have curl installed on your machine by running `curl -V`.


## Your first API SQL Download

The very [first example](https://techdocs.gbif.org/en/data-use/api-sql-downloads#requesting-an-sql-occurrence-download) as provided by GBIF should work fine. In the _curl_ command, just replace `YOUR_GBIF_USERNAME` and `YOUR_PASSWORD` with your credentials. In the [`query.json`](https://github.com/damianooldoni/b3cubes-sql-examples/blob/main/examples/examples_gbif/query.json) file, please replace `"userEmail@example.org"` with your email address, or remove the `notificationAddresses` and set `"sendNotification": false`.

```
curl --include --user YOUR_GBIF_USERNAME:YOUR_PASSWORD --header "Content-Type: application/json" --data @query.json https://api.gbif.org/v1/occurrence/download/request
```

Notice that you can give another name than `query.json` to the file containing the SQL query. So, if you cloned this repository and are in folder `./examples/examples_gbif`, you can replace `@query.json` with `@[other_name_than_query.json](https://github.com/damianooldoni/b3cubes-sql-examples/blob/main/examples/examples_gbif/other_name_than_query.json)` and the same download will be triggered again: a "cube" with the number of occurrences from Europe per dataset and country will be generated again, with a new DOI and `downloadKey`:

```
curl --include --user YOUR_GBIF_USERNAME:YOUR_PASSWORD --header "Content-Type: application/json" --data @other_name_than_query.json https://api.gbif.org/v1/occurrence/download/request
```

Tip: use always a **meaningful filename**. `query.json` is good for a first test, but not more than that :-)

Notice also that you can generate the same download by running the curl commands from another directory. For example, if you are in the root directory of this gitHub repository and you are on a Windows machine, using `@examples\examples_gbif\query.json` in the curl command will do the job:

```
curl --include --user YOUR_GBIF_USERNAME:YOUR_PASSWORD --header "Content-Type: application/json" --data @examples\examples_gbif\query.json https://api.gbif.org/v1/occurrence/download/request
```

As shown on GBIF documentation page, you can make use of the [Query Validation](https://techdocs.gbif.org/en/data-use/api-sql-downloads#sql-validation) tool, before triggering a download. Handy, isn't?


## Your first species occurrence cube

The main reference to build your first species occurrence cube is the [Species occurrence cubes](https://techdocs.gbif.org/en/data-use/data-cubes) page on Tech Docs of GBIF.

You can run your first species occurrence cube by slightly manipulating the final SQL query in Section [Write Full Query](https://techdocs.gbif.org/en/data-use/data-cubes#write-full-query). You will have to:
- Replace double quotes, `"`, with `\"`, e.g. `\"year\"`.
- Remove comments, e.g. `-- Dimensions:`

You can find the final json file, [`cube_test.json`](https://github.com/damianooldoni/b3cubes-sql-examples/blob/main/examples/examples_gbif/cube_test.json), in [`examples/examples_gbif`](https://github.com/damianooldoni/b3cubes-sql-examples/tree/main/examples/examples_gbif) directory. Submit the request as we did it before:

```
curl --include --user YOUR_GBIF_USERNAME:YOUR_PASSWORD --header "Content-Type: application/json" --data @examples\examples_gbif\cube_test.json https://api.gbif.org/v1/occurrence/download/request
```

I also asked to add the final adjusted query to the [Species occurrence cubes](https://techdocs.gbif.org/en/data-use/data-cubes) page, see issue [tech-docs#97](https://github.com/gbif/tech-docs/issues/97).

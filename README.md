# how-to-bind-command-in-.net-maui-accordion

**Repository Description**  
This repository contains a .NET MAUI sample that demonstrates how to bind a `Command` to items generated inside the Syncfusion **SfAccordion** control.

The sample illustrates a practical pattern for invoking page‑level commands from within dynamically generated accordion item templates using `BindableLayout.ItemsSource` and `x:Reference`.

## Project Overview
The purpose of this project is to help developers understand how to connect view‑model commands to UI elements inside `SfAccordion` items in a .NET MAUI application. It demonstrates a clean MVVM‑friendly approach for handling item‑level interactions—such as button clicks—while keeping logic in the page’s view model.

## Features
- Integration of Syncfusion .NET MAUI SfAccordion  
- Bind data using `BindableLayout.ItemsSource`  
- Invoke page‑level `ICommand` from inside accordion item templates  
- Pass the current item as a `CommandParameter`  
- Use `x:Reference` to access the accordion’s binding context  

## Prerequisites
Ensure the following requirements are met before running the sample:
- Visual Studio 2022  
- .NET SDK compatible with .NET MAUI  

## Installation and Running the Project
1. Clone or download this repository to your local machine.
2. Open the solution file in Visual Studio 2022.
3. Restore NuGet packages by rebuilding the solution.
4. Build and run the project on a supported .NET MAUI platform.

## Configuration

This sample demonstrates how to bind a Command to items generated inside a Syncfusion `SfAccordion` in a .NET MAUI application. 


Below is the exact XAML used in this sample to wire the command from the page's view-model into the generated item template. Note how the `ImageButton` binds `Command` to `BindingContext.ShowDetailsCommand` on the `SfAccordion` reference and passes the current item as the `CommandParameter`.
**XAML
```
<ContentPage.BindingContext>
    <local:ItemInfoRepository x:Name="viewModel" />
</ContentPage.BindingContext>

<accordion:SfAccordion x:Name="accordion"
                        BindableLayout.ItemsSource="{Binding Info}"
                        ExpandMode="SingleOrNone">
    <BindableLayout.ItemTemplate>
        <DataTemplate>
            <accordion:AccordionItem>
                <accordion:AccordionItem.Header>
                    <Grid Padding="5,0,0,0"
                            HeightRequest="50">
                        <Label Text="{Binding Name}"
                                FontSize="20" />
                    </Grid>
                </accordion:AccordionItem.Header>
                <accordion:AccordionItem.Content>
                    <Grid BackgroundColor="#C0C0C0"
                            Padding="5,0,0,0">
                        <Grid.ColumnDefinitions>
                            <ColumnDefinition Width="*" />
                            <ColumnDefinition Width="65" />
                        </Grid.ColumnDefinitions>
                        <Label Text="{Binding Description}"
                                VerticalOptions="Center" />
                        <Grid Grid.Column="1"
                                Padding="10"
                                BackgroundColor="#C0C0C0">
                            <ImageButton BackgroundColor="{OnPlatform WinUI=#C0C0C0}"
                                            Source="details.png"
                                            Command="{Binding Path=BindingContext.ShowDetailsCommand, Source={x:Reference accordion}}"
                                            CommandParameter="{Binding .}" />
                        </Grid>
                    </Grid>
                </accordion:AccordionItem.Content>
            </accordion:AccordionItem>
        </DataTemplate>
    </BindableLayout.ItemTemplate>
</accordion:SfAccordion>
```
### How it works 
- The `ContentPage.BindingContext` is set to an instance of `ItemInfoRepository` (the view-model). That view-model exposes an `Info` collection and a `ShowDetailsCommand`.
- `BindableLayout.ItemsSource` creates one `AccordionItem` per element in the `Info` collection; each generated item's BindingContext is the item itself.
- Inside the item template, the `ImageButton` cannot see the page-level command directly because its DataContext is the item. Using `Source={x:Reference accordion}` and then `BindingContext.ShowDetailsCommand` accesses the page's command and allows the item to pass itself as the parameter (`CommandParameter={Binding .}`).


## Usage
Run the application and expand an accordion item.  
Each item contains an `ImageButton` that triggers a **page‑level command** (`ShowDetailsCommand`) defined in the view model. The current data item is passed as the command parameter, enabling contextual actions such as displaying item‑specific information.

## Documentation
- General Syncfusion documentation:
https://help.syncfusion.com/
- .NET MAUI Introduction:
https://help.syncfusion.com/maui/introduction/overview
- .NET MAUI Accordion Getting Started:
https://help.syncfusion.com/maui/accordion/getting-started

## Additional Resources
- Syncfusion MAUI Accordion feature overview:
https://www.syncfusion.com/maui-controls/maui-accordion

## Troubleshooting
- Ensure the page’s BindingContext is correctly set before initializing the accordion.
- Verify the x:Reference name matches the SfAccordion control.
- Rebuild the solution if command bindings do not trigger.
- Check output logs for binding or runtime errors.

## Conclusion

I hope you enjoyed learning about how to bind a Command to items in .NET MAUI Accordion(SfAccordion).

You can refer to our [.NET MAUI Accordion](https://www.syncfusion.com/maui-controls/maui-accordion) feature tour page to know about its other groundbreaking feature representations. You can also explore our [.NET MAUI Accordion documentation](https://help.syncfusion.com/maui/accordion/getting-started) to understand how to present and manipulate data.

For current customers, you can check out our components from the [License and Downloads](https://www.syncfusion.com/account/login) page. If you are new to Syncfusion, you can try our 30-day [free trial](https://www.syncfusion.com/downloads/maui) to check out our other controls.

If you have any queries or require clarifications, please let us know in the comments section below. You can also contact us through our [support forums](https://www.syncfusion.com/forums/), [Direct-Trac](https://support.syncfusion.com/create), or [feedback portal](https://www.syncfusion.com/feedback/maui?control=sflistview). We are always happy to assist you!

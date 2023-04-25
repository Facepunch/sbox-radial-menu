# sbox-radial-menu
🥧 A reusable and customizable radial menu for use in games.

# Example Usage

## C# Code

```csharp
using Sandbox;
using Sandbox.UI;
using System.Linq;
using Conna.RadialMenu;

namespace Facepunch.Hidden
{
	[StyleSheet( "/ui/RadialVoiceMenu.scss")]
	public partial class RadialVoiceMenu : RadialMenu
	{
		public override string Button => "view";

		public override void Populate()
		{
			var commands = ResourceLibrary.GetAll<RadioCommandResource>().ToList();

			foreach ( var command in commands )
			{
				AddRadioCommand( command.Text, command.ResourceId );
			}
		}

		protected override bool ShouldOpen()
		{
			return Game.LocalPawn is HiddenPlayer player && player.Team is IrisTeam;
		}

		private void AddRadioCommand( string name, int resourceId, string icon = null )
		{
			AddItem( name, "Play through radio", string.IsNullOrEmpty( icon ) ? "ui/icons/icon-ability-2.png" : icon, () => HiddenPlayer.PlayVoiceCmd( resourceId ) );
		}
	}
}
```

## CSS

```css
@import "BaseRadialMenu.scss";

.radial-menu {
    border-color: rgba( seagreen 0.6 );

    .dot {
        background-color: lighten( seagreen, 0.4 );
        box-shadow: 0px 0px 4px 4px rgba( seagreen, 0.2 );
    }

    .items {
        RadialMenuItem {
            background-color: rgba( seagreen 0.6 );
        }
    }

    .center {
        .info {
            .name {
                font-family: Lexend;
                font-size: 32px;
                text-shadow: 0px 0px 4px rgba( seagreen, 0.2 );
                color: lighten( seagreen, 0.4 );
            }

            .description {
                font-family: Lexend;
                font-size: 20px;
                color: white;
            }
        }

        .arrow {
            background-tint: green;
        }
    }
}
```

# Twitter-bot-
using System;
using TweetSharp;

namespace TwitterBot
{
    class Program
    {
        private static string customer_key = "9Uy9RxtD4B8b5sKN6KrEJinXC";
        private static string customer_key_secret = "xRsCbi7WOus9DAxJEMrWHoaCHLrxSdaFucmVcBO05k24C25U6s";
        private static string access_token = "80354208021891072-ucSJaXm5T9VGF4HugcQ31UqTytn9Kud";
        private static string access_token_secret = "OHSITGdWxIXibm8YToP9Y5foB3DYYQjtFr38zEfFpaxP";

        private static TwitterService service = new TwitterService(customer_key, customer_key_secret, access_token, access_token_secret);
        static void Main(string[] args)
        {
            Console.WriteLine($"<{DateTime.Now}>-Bot Started");
            SendTweet("Hello World");
            Console.Read();
        }
        private static void SendTweet(string _status)
        {
            service.SendTweet(new SendTweetOptions { Status = _status }, (tweet, response) =>
            {
                if(response.StatusCode == System.Net.HttpStatusCode.OK)
                {
                    Console.ForegroundColor = ConsoleColor.Green;
                    Console.WriteLine($"<{DateTime.Now}>-Tweet sent!");
                    Console.ResetColor();
                }
                else
                {
                    Console.ForegroundColor = ConsoleColor.Red;
                    Console.WriteLine($"<ERROR>" + response.Error.Message);
                    Console.ResetColor();
                }
            });
        }
    }
}
